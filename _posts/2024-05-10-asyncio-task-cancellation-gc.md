---
title: "Garbage Collect for Asyncio Task Instance cancelled in Python"
last_modified_at: 2025-01-07T00:00:00-09:00
categories:
- Asyncio
tags:
- python
- gc
- garbage-collection
excerpt: "Python Asyncio Task를 cancel하면 GC가 적절히 처리하는가? 그리고 어떻게 Cancel 할 때 GC 성능이 제일 좋은지도 측정해보자"
---

## "Asyncio Task를 cancel하면 garbage-collection 되는가?"

### 된다

Work는 무한 Sleep 상태의 Task로 한다.
`Task`를 생성하고 즉시 `cancel` 했을 때(test1), 모아서 한번에 `cancel` 했을 때(test2),
`cancel` 하지 않았을 때(test3)의 경우에 대해서 테스트한다. test4는 아무것도 동작하지 않은 경우를
비교군에 추가한다.

겸사겸사 성능 테스트도 해본다. Object 크기와 GC threshold를 조절해가며 비교한다.


### 테스트 코드

```python
import tracemalloc
import asyncio
from contextlib import contextmanager, suppress
import gc
import time

gc.set_threshold(700, 10, 10)

TEST_COUNT = 100000

class Work:
    """Work structure."""
    __next_index = 1000

    def __init__(self, func, *args, **kwargs):
        self.index = self.__new_index()
        self.func = func
        self.args = args
        self.kwargs = kwargs

    async def run(self):
        await self.func(*self.args, **self.kwargs)

    @classmethod
    def __new_index(cls) -> int:
        index = cls.__next_index
        cls.__next_index += 1
        return index

class WorkScheduler:
    def __init__(self):
        self.__works: dict[int, asyncio.Task] = {}

    def register(self, loop: asyncio.AbstractEventLoop, work: Work) -> None:
        task = loop.create_task(work.run())
        task.add_done_callback(lambda _: self.unregister(work.index))
        self.__works[work.index] = task

    def unregister(self, index: int) -> None:
        with suppress(KeyError):
            task = self.__works.pop(index)
            task.cancel()

    def stop(self) -> None:
        for task in self.__works.values():
            task.cancel()

        self.__works.clear()

async def func():
    await asyncio.sleep(1000)

async def test1(wq):
    for i in range(TEST_COUNT):
        work = Work(func)
        wq.register(asyncio.get_running_loop(), work)
        await asyncio.sleep(0)
        wq.unregister(work.index)

async def test2(wq):
    for i in range(TEST_COUNT):
        work = Work(func)
        wq.register(asyncio.get_running_loop(), work)
    await asyncio.sleep(0)
    wq.stop()

async def test3(wq):
    for i in range(TEST_COUNT):
        work = Work(func)
        wq.register(asyncio.get_running_loop(), work)
    await asyncio.sleep(0)

async def test4(wq):
    await asyncio.sleep(0)

@contextmanager
def monitoring():
    tracemalloc.start()

    before = time.time()
    yield
    after = time.time()
    print("running time:", after - before)

    print("using memory(curr, peak):", tracemalloc.get_traced_memory())
    tracemalloc.stop()

    obj = gc.get_count()
    gc.collect()
    print("gc object (before, after collect):", obj, gc.get_count())
    print()


for f in [test1, test2, test3, test4]:
    wq = WorkScheduler()
    with monitoring():
        asyncio.run(f(wq))
    wq.stop()
    del wq
```


### 결과

#### OBJ count 100000, gc threshold 700, 0, 0

```
running time: 2.615762233734131
using memory(curr, peak): (5703, 18072)
gc object (before, after collect): (54, 0, 0) (0, 0, 0)

running time: 4.3394060134887695
using memory(curr, peak): (4437124, 255157752)
gc object (before, after collect): (0, 1, 12) (0, 0, 0)

running time: 5.501044988632202
using memory(curr, peak): (5363972, 282053740)
gc object (before, after collect): (0, 0, 19) (0, 0, 0)

running time: 0.0011508464813232422
using memory(curr, peak): (1980, 8024)
gc object (before, after collect): (32, 0, 0) (0, 0, 0)
```

#### OBJ count 100000, gc threshold 700, 0, 0

```
running time: 2.5128602981567383
using memory(curr, peak): (4767, 17184)
gc object (before, after collect): (43, 1, 3) (0, 0, 0)

running time: 4.085307598114014
using memory(curr, peak): (4437124, 255149832)
gc object (before, after collect): (0, 2, 11) (0, 0, 0)

running time: 5.38167667388916
using memory(curr, peak): (5490036, 282023204)
gc object (before, after collect): (0, 7, 29) (0, 0, 0)

running time: 0.0011458396911621094
using memory(curr, peak): (1980, 8024)
gc object (before, after collect): (32, 0, 0) (0, 0, 0)
```

#### OBJ count 1000000, gc threshold 700, 0, 0

```
running time: 25.805277347564697
using memory(curr, peak): (5703, 18072)
gc object (before, after collect): (54, 0, 0) (0, 0, 0)

running time: 43.80046892166138
using memory(curr, peak): (33797252, 2543382440)
gc object (before, after collect): (0, 1, 387) (0, 0, 0)

running time: 58.940531730651855
using memory(curr, peak): (42190204, 2802028988)
gc object (before, after collect): (0, 1, 1582) (0, 0, 0)

running time: 0.00410771369934082
using memory(curr, peak): (1980, 8026)
gc object (before, after collect): (32, 0, 0) (0, 0, 0)
```

#### OBJ count 1000000, gc threshold 700, 10, 10

```
running time: 25.59279990196228
using memory(curr, peak): (4767, 17184)
gc object (before, after collect): (43, 1, 3) (0, 0, 0)

running time: 46.78571057319641
using memory(curr, peak): (33797252, 2543382440)
gc object (before, after collect): (0, 4, 18) (0, 0, 0)

running time: 56.32780623435974
using memory(curr, peak): (42190204, 2802028988)
gc object (before, after collect): (0, 5, 347) (0, 0, 0)

running time: 0.003941535949707031
using memory(curr, peak): (1980, 8026)
gc object (before, after collect): (32, 0, 0) (0, 0, 0)
```


실행 후 매번 바로 삭제하는 것이 메모리 적으로도 실행시간 적으로도 이득이며, cancel 후 따로 await
하지 않아도 메모리가 해제된다는 것을 알 수 있다. 또한 인스턴스 숫자가 많아질 수록 당연하게도 gc에
소모되는 클럭이 많아지는 것으로 보여진다.
