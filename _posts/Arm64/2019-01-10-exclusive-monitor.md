---
title: "Exclusive Monitor and LDXR/STXR Instruction"
last_modified_at: 2019-01-12T02:20:10-09:00
categories:
- Synchronization
tags:
- arm64
- synchronization
- exclusive
- instruction
- memory access
- deadlock
excerpt: "Exclusive Monitor and Instruction"
---

## Exclusive Monitor (배타적 모니터)란?
메모리 load/store 시에 그 데이터에 대한 동기화를 위한 작업으로, 메모리를 load하는
순간부터 store하는 순간 까지 다른 core나 thread가 해당 데이터를 access 하였는지
모니터링 하는 시스템이다.
**즉**, load/store 시에 값이 동일 하다는 것을 다른 task나 core에 대해 exclusive하게
synchronize 하다. ~~_반복해서 설명하는 것 같지만_~~ 이 데이터는 load부터 store 시까지
완벽하게 일관성, 원자성을 유지하겠다는 의미이다. (DB의 transaction 처럼)

이 명령에 대한 예제로 simple spin lock 구현이 [ARMv8 synchronization primitives](https://static.docs.arm.com/100934/0100/armv8_a_synchronization_primitives_100934_0100_en.pdf) 7번 페이지에 등장~

## Exclusive Instruction

ARMv7과 ARMv8은 shared memory에 대해 blocking 하지 않는 동기화를 지원하는 명령이 존재. **load / store exclusive instruction 계열** (ldxr/stxr or ldrex/strex) <br>
blocking 하지 않음 == 동기화가 이루어질 때까지 어떠한 core나 task가 기다리지 않음.

**LDXR**
- exclusive monitor에 exclusive access tag를 지정하면서 memory load를 수행한다.
- `LDXR R0, [X0]` : R0에 X0 위치의 데이터를 load

**STXR**
- 해당 데이터에 대해 exclusive 상태이면 memory store를 수행. 즉, LDXR이 이미 수행되어야만 하며, LDXR과 STXR이 진행되는 사이에 다른 core나 task에 의해 해당 데이터가 access되어 open 상태가 되면 실패한다.
- 실패를 하면 실패했다는 값을 넘겨주고, blocking 하지는 않음.
- `STXR W0, R0, [X0]` : 성공 시, W0에 zero return, R0의 데이터를 X0 위치에 store. 실패 시, W0에 non-zero return, store 실패.

## Exclusive Monitor

### Local monitor
- 각 코어마다 존재.(L1 memory)
- 한 코어 내에서 서로 다른 태스크가 같은 주소 공간의 메모리에 접근 하고자 하는 것을 monitoring. (= Concurrency) 
- 선점으로 인한 exclusive access 깨지는 것을 monitoring한다.
- 다른 task가 해당 데이터를 변경(store)하게되면 배타적 접근은 깨졌다는 것으로 판단. (task마다 기록하는 것이 아님.)
- 구현이 프로세서마다 다름.
> The CLREX instruction clears the monitors, but unlike in ARMv7-A, exception entry or return also does the same thing. The monitor can also be cleared in error, for example by cache evictions or other reasons that are not directly related to the application. Software must avoid having any explicit memory accesses, system control register updates, or cache maintenance instructions between paired LDXR and STXR instructions.

### Global monitor 
- 여러 코어를 연결하는 메모리(L2 memory) 간에 한 개 이상 존재. 공유한다.
- 각 코어 내에서 동시에 메모리에 접근 하고자 하는 것을 monitoring. (= Parallelism.)
- 그러나 동시각은 아니어도 됨. 서로 다른 코어에서 접근을 모니터링 하는 것을 목적 
- 각 master(core)마다 배타적 접근을 관찰. 즉, 어느 코어가 배타적 접근을 수행하였는지 알고있음. (core마다 기록.)

![default](https://user-images.githubusercontent.com/24751868/51051487-3de53080-1617-11e9-9f1f-d4ff5743464f.PNG)
> 출처: <https://developer.arm.com/docs/100898/latest/memory-access-instructions>

**Notice**: 캐시와 매우 밀접한 것 같지만, 서로 다른 역할을 하는 별도의 모듈로 생각해야함.
캐쉬에서 말하는 독점 상태와 구별 할 수 있어야함.
(캐시의 구현에 독점 모니터도 함께 거론될 정도로 밀접함)
{: .notice--info }


## LDXR/STXR 사이에 Deadlock이 발생 할까?

멀티코어 시스템에서 양 core는 동일한 cpu clock에 다른 task에 의한 preempt가 없고
interrupt가 발생하지 않는다고 가정했을 때, 뒤에 보이는 코드를 양 core가 약간의 
instruction 차이로 접근한다면 "deadlock이 발생할 수 있지 않을까" 라는 가설을 세움.
(+ 왜냐하면 ldxr의 명령은 다른 시스템의 exclusive tag가 clear될 것으로 착각함.)

~~_It is technically possible yes!_~~
**+ 아니란다.**

```
.spin_lock:
        NOP
.stxr_fail:
        LDXR  R0, .data+0
        CMP   R0, #0
        BNE    .spin_lock
        MOV  R0, #1
        STXR  W0, R0, .data+0
        CMP   W0, #0
        BNE   .stxr_fail
        BL       critical_section()
        MOV  R0, #0
        STR     R0, .data+0
        RET 
.data:
        .word lock
```

![exclusive spin lock 1](https://user-images.githubusercontent.com/24751868/50984165-897ada00-1544-11e9-92fd-061bef3a12b4.PNG){: .width="100%" }

양쪽 코어는 동일한 클럭 속도로, 동일한 코드를 약간의 차이로 계속 반복하며 동작하는 예제이다.
동작은 번호 순서대로 진행되며, 같은 색의 선은 atomic하게 동작한다고 가정한다. :

![exclusive spin lock 2](https://user-images.githubusercontent.com/24751868/50984167-8b449d80-1544-11e9-9a4a-9e2527d968ae.PNG){: .width="100%" }

### 결론

~~_기술적으로는 가능한 일이나, 현실적으로 신경써야 할 정도로 큰 문제가 발생하지 않는다는 결론이다.
선점, 혹은 인터럽트 등을 비롯하여 현실적으로 양 코어가 완벽히 저런 데드락 상태에
오래 지속되지 않으며, 그 짧은 데드락 상태 조차도 거의 일어나지 않는다.
몇 번의 루프 동안의 데드락이 발생할 수 있으나 현실적으로 시스템에 큰 영향을 주지는
아니하므로 위 데드락 상태에 대한 가능성은 무시한다._~~

관련 질문은 아래에 링크로 걸었다시피 **직접** 해보았다.

> <https://stackoverflow.com/questions/54103521/do-exclusive-load-and-store-arm-instruction-raise-a-deadlock>

### 변경사항

**+ 불가능하단다.** 
Exclusive Monitor의 exclusive-access tag의 clear는 오로지 해당 공간에 대한 store. 즉, 변경에 의해서만 발생한단다.
(혹은 CLRX instruction. clear 시킨다는 뜻이다.)
두 master가 동시에 exclusive load(access)가 가능하단다. 각자 master마다 해당 주소에 대해 exclusive tag를
모두 가질 수 있기 때문에, 먼저 store 하는 사람이 이긴다. (동시에 store하는 경우는 추후에 업데이트하겠음..)

하지만 위에 적은 내용들은 하드웨어 구현 따라 달라질 수 있는 내용이고, 이 내용은 하드웨어 칩에
완전히 종속적이고 밀접하기 때문에, 사용하기 전에 하드웨어 master(like core)의 레퍼런스 문서를
참조 하고 나서 사용하기를 조언받음.




## LDR/STR과 LDXR/STXR은 차이가 뭘까?

- LDR : 메모리를 load 한다.
- STR : 메모리를 store 한다.
- LDXR : LDR의 동작을 수행하며 exclusive monitor에 access tag를 set한다.
- STXR : exclusive monitor에 access tag가 set 되어있으면 STR 동작을 하며 첫 번째 인자에 0을 리턴하고  access tag를 clear한다. clear 되어있으면 STR 동작은 실패하며 첫 번째 인자에 0이 아닌 값을 리턴한다.
