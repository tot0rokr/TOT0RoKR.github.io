---
title: "ISB/DMB/DSB barrier & ordering & pipeline"
last_modified_at: 2019-08-06T21:47:00-09:00
categories:
- Barrier
tags:
- barrier
- memory
- instruction
- pipeline
- memory ordering
- execution ordering
excerpt: "instruction barrier인 ISB 명령과 data barrier인 DMB/DSB 명령에 대한 자세한 설명과 예시. cpu 최적화인 ordering 기법과 pipeline에 대한 설명."
---

## Introduce

**Arm64 아키텍처**에서 사용되는 **barrier**의 machine code에 해당하는 **instruction**인
**ISB / DMB / DSB** 에 대해서 설명한다.

그 전에 알아야 하는 **pipeline**과 cpu level에서 수행하는 최적화인 **ordering**에
대해서 살펴본다.


## Processing instructions

**Instruction**은 cpu가 처리하는 명령어에 해당하는 용어입니다.
한 instruction이 동작하기 위해서는 보통 5단계(아키텍처마다 다름)의 과정을 거쳐서 수행됩니다.
이 5단계가 다 거쳐야지 한 instruction이 수행되었다고 말하구요. 이 한 단계의 과정이 소요되는 시간을
1 cpu clock이라고 부릅니다. 즉, 한 instruction은 처리되는데 총 5 clock이 소요되는 것이지요.

이 5단계는:

- IF(Instruction Fetch 명령어인출)
- DE(Decode 명령어 해독 + 레지스터 Read)
- EX(Execution 산술/논리 연산 수행)
- MEM(Memory Access 메모리 접근 read/write)
- WB(Write Back 레지스터 Write)

로 구성됩니다.

#### IF

IF는 메모리에서 명령어를 읽어오고 PC(program counter) 혹은 IP(instruction pointer)를
다음 명령어를 가리키게 합니다.


#### DE

DE는 명령어를 해독합니다. 비트단위로 쪼개서 어떤 instruction 인지 보고 그에 해당하는
제어신호를 보내 instruction을 처리합니다. 또한 operand로 들어온 레지스터를 read합니다.


#### EX

EX는 산술(덧,뺄,곱,나눗셈), 논리(AND, OR, NOT) 등을 수행합니다.
coprocessor(보조프로세서)를 이용해 캐시, MMU 등을 컨트롤하거나 SIMD, 부동소숫점
연산을 수행하기도 합니다.


#### MEM

MEM은 메모리 접근을 수행합니다. Memory에 R/W하는 동작은 여기서 이루어집니다.


#### WB

WB은 레지스터 쓰기를 수행합니다. Mem단계에서 읽어온 메모리의 값을 레지스터에
쓰거나, EX 단계에서 add 등을 이용해 연산된 결과를 레지스터에 저장할 때 사용됩니다.



## Pipeline

**pipeline(파이프라인)**은 이 5단계를 쉬지 않고 연이어 실행하는 겁니다.
즉 최대 instruction 5개가 동시에 수행되는 겁니다.

예를 들면 "빨래"라는 instruction을 수행한다고 가정하면 "세탁", "건조", "정리"의 단계는
서로 독립적이기 때문에 최대 세탁이 가능한 빨래를 동시에 3묶음을 처리할 수 있는 것과
같습니다.


### Hazard

그런데 문제가 발생합니다. 레지스터에 쓰기는 5단계에서 수행하는데, 읽기는 2단계에서
수행됩니다. 즉,

``` assembly
ldr r0, [sp+1000]
add r1, r1, r0
```

와 같은 구문이 있을 때, `ldr`를 통해 메모리에서 읽은 값을 `r0`에 쓰기 위해서는 WB 단계에서
가능합니다. 그런데 그 때가 되면 이미 `add`라는 명령은 파이프라인에 의해 레지스터를 읽는
DE단계와 `add`명령을 수행하는 EX단계가 끝나고 MEM단계에 이른 상태일 것입니다.
이것을 **"Hazard(해저드)"** 발생이라고 부릅니다.
(Hazard는 structural/data/control 세 가지가 존재하지만 설명은 생략합니다.)

물론 그러면 안 되기 때문에 파이프라인은 중지되고, `ldr`명령이 WB단계가 끝날 때까지
`add`명령은 중지됩니다.(진행되지 않고 쉽니다.) 즉 2 클럭동안 **"stall(스톨)"** 되었다고 부릅니다.


### Execution ordering

이 방법을 해결하기 위한 방법이 여러가지가 있는데, 그 중 하나는 의존성이 없는 다른
instruction을 `ldr`과 `add` 사이에 끼워넣는 방법입니다. `ldr` 위에 있는 instruction이나,
`add` 아래있는 instruction 중, 예를 들면,

``` assembly
ldr r0, [sp+1000]
add r1, r1, r0
ldr r2, [sp+2000]
add r2, r2, r2
ldr r3, [sp+3000]
```

이렇게 구성된 구문을 

``` assembly
ldr r0, [sp+1000]
ldr r2, [sp+2000]
ldr r3, [sp+3000]
add r1, r1, r0
add r2, r2, r2
```

이렇게 stall 될 수 있는 클럭 만큼 위아래 다른 위치의 instruction을 dependency를
해지치 않는 한에서(해칠 수 있으나, cpu 입장에서 해치지 않는다고 판단하면)
instruction간에 순서를 바꿉니다.(실행 도중 cpu가 자기맘대로 바꾸는 것)
이것을 **Instruction ordering** 혹은 **Execution ordering**이라고 부릅니다.


### ISB (instruction synchronization berrier)

ISB는 instruction ordering을 막고,
pipeline을 flush 시킵니다. 즉, `isb`가 수행이 완료되었을 때
(EX 단계일지, WB단계일지는 cpu 설계자가 아니라 저도 잘 모르겠음. 아마도 EX단계)
`isb` 다음에 있는 모든 명령에 대해서 pipe line을 flush 시켜서 IF 단계부터 다시 수행하게
만드는 **barrier** 입니다. 그렇게 되면 `isb` 명령어 앞에서 실행된

- CP15 레지스터에 대한 변경,
- ASID(Address Space IDentifier) 변경
- 완료된 TLB 유지관리 작업
- branch prediction(분기 예측기) 작업

과 같은 컨텍스트 변경 작업의 효과가 `isb` 뒤의 명령에 영향을 미칩니다.

SY를 유일한 option으로 가지며, default 값이고, 생략 가능합니다.



## Accessing memory

### Memory ordering

메모리를 접근할 때, cache hit(캐시 적중)이나 momory burst mode 등의 여러가지 이유로
"인접한" 주소를 access 하는 것이 멀리 떨어진 주소를 access 하는 것보다 빠릅니다.
그렇기 때문에, 인접한 주소에 대한 memory access를 수행하는 instruction을 모아서
처리하기도 합니다.(cpu 맘대로)

어셈으로 예를 들면,

``` assembly
str r0, [sp+1000]
ldr r1, [sp+2000]
and r1, #11
str r2, [sp+1004]
ldr r3, [sp+1996]
and r3, #8
```

이런 구문이 있다고 가정하겠습니다. 이 동작을 "Optimization"하게되면 cpu는

``` assembly
str r0, [sp+1000]
str r2, [sp+1004]
ldr r3, [sp+1996]
ldr r1, [sp+2000]
add r0, r1, r0
add r4, r2, r3
```

하게 순서를 바꿀 수 있습니다. 그런데 문제는 [sp+1004]번지의 데이터를 쓰는 것이
[sp+2000]번지의 데이터를 읽는 것에 영향을 줄 수 있습니다. **dependency**가 존재한다는
것이죠.
물론, 일반적인 상황에서는 일어나지 않습니다만 [sp+1000~2000]번지가 device를 접근하기
위한 주소라면 이야기가 다릅니다. device의 i/o(input/output)을 위해 메모리 주소를
이용합니다. (이 방식을 **memory mapped I/O** 라고 부릅니다.)

즉 [sp+1004]번지에 데이터를 변경하게 되는 것은 device의 상태를 변경 시키게 되고,
처음과 다른 상태에서 [sp+2000]번지의 데이터를 읽게 될 수도 있다는 이야기입니다.
dependency가 존재한다는 것이죠.
이것은 device에 종속된 문제기 때문에 cpu는 전혀 알 수 없습니다. 그렇기 때문에
위 사례처럼 바꾸어 버리는 사태가 벌어질 수 있습니다.


### DMB (Data memory barrier)

DMB는 그렇기 때문에 만들어 졌습니다.
`dmb` instruction은 memory에 대한 access의 순서가 `dmb` 위 아래로 memory access의
순서가 변경되지 않음을 보장합니다. 즉 위에서 말한 사태가 벌어지지 않기 위해서

``` assembly
str r0, [sp+1000]
ldr r1, [sp+2000]
and r1, #11
dmb
str r2, [sp+1004]
ldr r3, [sp+1996]
and r3, #8
```

이런식으로 구성하면 되겠죠.
물론 위와 같은 상황에선 인접한 `str`과 `ldr`의 순서도 바뀔 가능성이 전혀 없는 것은 아니기
때문에 (cpu 입장에서 의존성을 확인할 수 없으므로) 정확히 하기 위해서

``` assembly
str r0, [sp+1000]
dmb
ldr r1, [sp+2000]
and r1, #11
dmb
str r2, [sp+1004]
dmb
ldr r3, [sp+1996]
and r3, #8
```

이렇게 만들 수도 있습니다. `dmb`가 사용된 만큼의 clock동안 프로그램 자체가
수행되지 않으므로 느려질 수도 있지만요.

`dmb` instruction은 다른 instruction에 대해서는 전혀
건드리지 않습니다.


### DSB (Data synchronization barrier)

DSB는 DMB보다 강력한 도구입니다.
`dsb` instruction은 `dmb` instruction을 포함함과 동시에, `dsb`가 수행되는 순간에
(아마도 EX단계. 추측임) 다음 명령이 완료되기를 기다립니다. `isb`와 다르게
pipeline을 flush 시키지는 않습니다. 'stall'만 시키는 겁니다.

- instruction cache 및 data cache 조작: cache miss에 대한 처리나 smp 환경에서
sharing되고 있는 캐시라인에 대해, 무효화/독점/공유 상태 변경 등을 수행하는 것
- branch predictor cache flush: cpu는 파이프라인을 위해 분기 예측(반복문, 조건문 등)을
하는데, 여러 기법을 통해서 compare & branch 부분에서 어디로 분기할지
예측을 합니다.(분기할지 말지) 그에 대한 정보를 flush 한다고 보면 될 것 같습니다.
- `dmb` instruction이 수행하는 행위
- TLB(Translation lookaside buffer) 유지 및 조작: MMU가 virtual address를
physical address로 빠르게 translation 하기 위한 cache인데, 이를 조작하고 유지하는 것을
말합니다.

위에 설명한 4가지 동작이 "완료"가 될 때까지 stall합니다. cache 및 MMU 동작은 보통
coprocessor(보조프로세서)인 CP15의 담당인데, 그들의 동작과 `dsb` instruction 이전의
명령어들의 동작이 완료되기를 기다리는 것으로 보입니다.


### options

DSB와 DMB는 공통 옵션이 있습니다.

- `NSH`는 non-sharable 의 약자로, sharable 하지않는, 즉, `dsb` 명령이 동작하는 core에서만
독점해서 사용하고 있는 메모리의 접근에 대해서만 `dsb` 명령을 수행하겠다라는 뜻입니다.
- `SY`는 전체 System을 의미하며, default 값이고, 생략가능합니다.
- `ISH`는 in-sharable - SMP 환경에서 core끼리만 공유
- `OSH`는 out-sharable - MMU를 비롯한 다른 옵저버들 간에도 공유

여기에 ST가 붙으면 load를 제외한 store에 대한 명령에 대해서만 dsb 명령을
수행하는 것이라고 보면 될 것 같습니다.
