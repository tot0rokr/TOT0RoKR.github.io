---
title: "Graceful shutdown asyncio tasks in signal handling with Python"
last_modified_at: 2024-02-06T00:00:00-09:00
categories:
- Python
tags:
- async
- python
- loop
excerpt: "Python에서 비동기 작업을 수행할 때, 우아하게 프로세스를 종료하는 방법에 대해서 다룬다."
---


이 글은 처음 저수준 api를 사용할 때 문제가 생기던 부분을 찾아보기 위한 참고 문서이다.
무언가를 설명하기 위한 글이 아님을 미리 알린다.


### Schedule future before loop.stop()

문제가 되는 상황은, `loop.stop()` 이후에 event loop에 추가된 future 작업은 수행되지 않는다(다음 loop
실행 때 수행된다)는 것이다. 이러한 상황은 `loop.stop()` 수행 전에 future나 task를 등록하였을 때도
적용되는데, future 내부에서 다른 future를 수행하는 경우이다. 한 마디로, A future 등록 > loop 중단 >
A future 내에서 새로운 future 등록이 불가하다는 의미이다.


### Schedule future after loop.stop() in signal handling

 SIGNAL handler 등에서 `loop.stop()`을 수행 후 `loop.run_until_complete()` 등을 수행하면,
 동작을 수행하지 않는 상황이 생긴다. 예시를 통해 살펴보자.


```python
import asyncio
import signal
from functools import partial

async def cleanup():
    # Some tasks for cleanup and graceful shutdown.

def sig_handler(loop):
    loop.stop()
    loop.run_until_complete(cleanup())  # line 10. option 1
    loop.create_task(cleanup())         # line 11. option 2

loop = asyncio.get_event_loop()
loop.add_signal_handler(signal.SIGINT, partial(sig_handler, loop))
loop.run_forever()                      # line 15
loop.close()
```

위 예제와 같은 상황에서 `cleanup()` awaitable은 수행되지 않는다. 뿐만 아니라
`sig_handler()`는 종료되지 않는다. `run_forever()` 호출로 인해 프로세스의 제어권은 event
loop에게 전달되고, 오로지 Interrupt singal을 이용해서 간섭할 수 있다(다른 시그널은 일단 이
예시에서는 제외한다).

기대하는 동작은 SIGINT 수신 시, loop를 stop으로 중단하여 `run_forever()`를
탈출함과 동시에, 여러가지 비동기 처리에 대한 graceful shutdown을 수행하고 싶었을 것이다.
그러나 `loop.stop()`을 수행하는 즉시 loop가 중단되는 것이 아니라, 중단 후 `loop.run_forever()`의
수행이 반환될 때 종료된다. 때문에 10번 라인에서 `RuntimeError: This event loop is already running`
에러가 발생한다.

그렇다면 11번 라인은 어떤가? 안타깝게도 `loop.stop()`을 수행하면, 새로운 event loop queue를 생성하여
새로운 퓨처는 다음에 호출될 `loop.run_forever()`나 `loop.run_until_complete()`에서 수행된다.
즉, 이미 event loop queue에 이미 hanging 되어있는 콜백들만 실행하고 line 15번으로 반환될 운명이다.
즉, 11번 라인을 수행시키고 싶으면, 15번 라인 뒤에서 event loop를 한 번 더 실행시켜줘야 한다. 하지만
그렇게 하면 기대하던 signal handling을 이용한 graceful이 더이상 아니지 않은가?

당연히, line 10과 11을 바꿔도 마찬가지이다. 위 문제는 순서와 상관 없이 독립적인 문제이다.


### How to graceful shutdown for awaitable tasks using signal handling

그렇다면 어떻게 signal handling을 통해서 awaitable task 들을 graceful shutdown을 할 수 있을까?
위 두 가지 문제를 모두 해결해야한다. 예시를 보면 생각보다 간단할수 있다.


```python
import asyncio
import signal
from functools import partial

async def cleanup():
    # Some tasks for cleanup and graceful shutdown.

def sig_handler(loop):
    task = loop.create_task(cleanup())
    task.add_done_callback(loop.stop)

loop = asyncio.get_event_loop()
loop.add_signal_handler(signal.SIGINT, partial(sig_handler, loop))
loop.run_forever()                      # line 15
loop.close()
```

모든 clean up task들을 수행한 뒤 loop를 중단할 수 있도록 하는 것이다. 이 clean up에는 기존에
동작하던 task를 cancel 하고 `gather()` 등으로 future들을 수거하는 동작을 포함할 수 있다.


### How to graceful shutdown for awaitable tasks raising exception

`loop.run_forever()`로 동작 중 발생하는 예외는 `loop.run_forever()` 바깥으로 전파되지 않는다.
event loop에 등록된 각 future들은 독립적이며, 각 future를 실행한 상위 future로만 전파되기 때문이다.
그렇기에 동작하는 future들을 event loop 바깥에서 예외를 처리하기 위해서는
`loop.set_exception_handler()`를 통해 예외 처리를 수행해야한다. 다행이도 signal handling과 꽤나
유사하다.

```python
import asyncio
import signal

async def cleanup():
    # Some tasks for cleanup and graceful shutdown.

def exception_handler(loop, context):
    task = loop.create_task(cleanup())
    task.add_done_callback(loop.stop)

async def job():
    raise Exception

loop = asyncio.get_event_loop()
loop.set_signal_handler(signal.SIGINT, exception_handler)
loop.create_task(job())
loop.run_forever()                      # line 15
loop.close()
```

핸들러의 경우 (loop, context) signature를 갖는 callable이어야 한다. `job()`에서 예외가 발생하면
job()이 중단되고, `exception_handler()`가 호출된다. 모든 clean up task들을 수행한 뒤 loop를 중단하여
예외 발생 시 loop를 중단할 수 있다. 예외 정보에 대한 것은 context에 들어있으며
[공식문서](https://docs.python.org/3.11/library/asyncio-eventloop.html#asyncio.loop.call_exception_handler)에서
context에 대한 정보를 자세하게 살펴볼 수 있다.
