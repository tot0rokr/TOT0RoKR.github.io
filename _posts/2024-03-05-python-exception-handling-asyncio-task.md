---
title: "Handling exceptions that occur within asyncio tasks in the event loop"
last_modified_at: 2025-01-07T00:00:00-09:00
categories:
- Python
tags:
- async
- python
- loop
- exception
excerpt: "Python에서 비동기 태스크에 대한 exception 방법에 대해 기술한다."
---

이 글에서는 비동기처리를 위한 이벤트 루프에서 동작 중인 태스크에서 발생한 예외를 처리하는 방법을
다루고, 또한, 이벤트 루프의 예외 처리기로 전파하는 방법을 강구한다.

파이썬 3.11.7 버전을 기준으로 작성한다.


## set_exception_handler()

`set_exception_handler()`는 이벤트 루프에 예외 처리기를 등록하는 메소드이다. 아래 예시와 같은
방법으로 예외를 등록하며 예외 발생 시 호출된다. 다만, 태스크에서 발생한 예외에 대해서 문제가 있어
후술한다.

```python
import asyncio

def exception_handler(loop, context):
    print("exception handling: ", context["exception"])
    loop.stop()

def main():
    loop = asyncio.get_event_loop()
    loop.set_exception_handler(exception_handler)

    async def test(n):
        await asyncio.sleep(n)
        print(f"test({n})")
        raise Exception(f"test({n}) !!!!!!!!!!!!!!!!!!!!!!!!!!")

    runners = []
    runners.append(loop.create_task(test(3)))       # line 17
    k = loop.create_task(test(4))                   # line 18
    loop.create_task(test(5)                        # line 19

    loop.run_forever()

if __name__ == '__main__':
    main()
```

17/18번 라인처럼 태스크가 변수나 컨테이너에 할당되면, 내부에서 발생한 예외가 `exception_handler()`에
전파되지 않고 태스크 자료구조에 캡쳐된 상태로 존재한다. 사실 이 동작이 정상적인 동작으로 간주해야
한다. 그러나 19번 라인처럼 태스크 object가 변수나 컨테이너에 할당되지 않으면
`exception_handler()`에 전파되고, 전파되지 않고 기다리던 다른 task들의 exception이 Catch된다.
(19번 라인을 지우면 `loop`가 종료되지 않는다.)

~~원래는 19번 라인도 전파되면 안되는 게 올바른 동작처럼 보인다. 사실 변수에 담는 행위가 영향을 끼치면
안된다.~~
GC에 의해 수집되면서 exception이 Catch되는 것으로 보여진다. 실제로 `k`나 `runners`를 `del`한 경우에
exception이 발생한다.


## run_coroutine_threadsafe()

이벤트 루프 내에서 예외를 처리하는 것이 아니라, 이벤트 처리를 수행하는 메인 스레드와, 코루틴 동작을
수행하는 서브 스레드로 분할하는 방법이다.

```python
import asyncio
from threading import Thread

def main():
    loop = asyncio.get_event_loop()

    thread = Thread(target=loop.run_forever)
    thread.start()

    async def test(n):
        await asyncio.sleep(n)
        print(f"test({n})")
        raise Exception(f"test({n}) !!!!!!!!!!!!!!!!!!!!!!!!!!")

    fut = asyncio.run_coroutine_threadsafe(test(3), loop)
    try:
        print(fut.result())
    except Exception as e:
        print(fut.exception())
    loop.call_soon_threadsafe(loop.stop)

    thread.join()

if __name__ == '__main__':
    main()
```

비동기 처리를 위한 thread를 따로 두고, 메인 스레드에서 비동기 처리를 등록. 하지만 이 방법은 이벤트
루프의 `exception_handler()`에서 catch하는 것이 아니고, future를 통해서 메인 스레드에서 catch하는
방법이다. 이벤트 처리기를 메인 스레드에서 구현한다.

## add_done_callback()

asyncio Task의 callback 호출을 이용해서 이벤트 루프의 exception handler를 호출하는 방법이다.
이벤트 루프 내에서 clean-up 등에 필요한 처리를 수행해야할 때 사용할 수 있다.

```python
import asyncio
from threading import Thread

def exception_handler(loop, context):
    print("exception handling: ", context["exception"])
    loop.stop()

def main():
    loop = asyncio.get_event_loop()
    loop.set_exception_handler(exception_handler)

    async def test(n):
        await asyncio.sleep(n)
        print(f"test({n})")
        raise Exception(f"test({n}) !!!!!!!!!!!!!!!!!!!!!!!!!!")

    def callback(fut):
        if fut.exception() is not None:
            print("callback: " + str(fut.exception()))
            raise fut.exception()

    loop.create_task(test(3)).add_done_callback(callback)

    loop.run_forever()

if __name__ == '__main__':
    main()
```

태스크가 완료되면 등록된 callback을 수행하게 되는데, 이 callback에서 예외를 발생시키는 방법이다.
task의 코루틴에서 발생한 예외는 태스크에 캡쳐되어 태스크가 완료 상태가 되고, 이후
`add_done_callback()`을 이용해 추가된 callback을 순차적으로 수행하게 되는데, callback에서 발생한
예외는 이벤트 루프의 exception handler에게 전파되는 것을 이용한다.

물론 위 `run_coroutine_threadsafe` 예제와 함께 사용할 수 있다. ~~이 경우, 태스크를 실행하기 전
`wrapper()`의 exception을 catch하는 용도로 사용할 수 있다.~~ 사례 변경으로 삭제.
