---
title: "MOESI protocol"
last_modified_at: 2019-01-10T23:15:00-09:00
categories:
- Cache
tags:
- arm64
- cache
- multicore
- coherence
excerpt: "Cache Coherence를 맞추기 위한 protocol(MOESI)."
---


## MOESI protocol이란?

캐시 일관성(cache coherence)을 맞추기 위한 scheme. ARMv8 프로세서에서는 MOESI 프로토콜을 사용한다.
MOESI는 캐시 상태의 앞글자를 따서 만든 단어이다.

- M (modified) : 캐시 라인이 최신 데이터를 가지며, 다른 캐시 라인에는 존재하지 않는 데이터이다. 메모리와 다른 데이터를 가지고 있다.
- O (owned) : 메모리에 write-back 하지 않은 상태에서 다른 캐시가 해당 라인을 share 하는 상태이다. 데이터를 요청한 캐시에 데이터를 CCI를 통해 직접 보낸다. 메모리와 다른 데이터를 가지고 있다.
- E (exclusive) : 캐시 라인이 이 캐시에 존재하며, 메모리와 같은 데이터를 갖고있다. 다른 어느 캐시와도 share하고 있지 않다.
- S (shared) : 캐시 라인이 다른 캐시와 share 상태이다. 메모리와 같은 데이터일 필요는 없다. owned 상태 캐시 라인을 가져왔을 수 있다.
- I (invalid) : 캐시 라인이 무효화 된 상태이다. 즉, 이 데이터는 다른 core에 의해 변경되었다.


## MOESI Rules

![moesi-state-diagram-for-processor-p1](https://user-images.githubusercontent.com/24751868/50971151-a7394680-1526-11e9-906b-c33db35a2c92.png)

> 출처 : https://www.researchgate.net/figure/MOESI-State-Diagram-for-processor-P1_fig8_318860805

- P1 core가 데이터를 수정. : P1의 캐시 라인은 M , 다른 core들의 캐시 라인은 I 
- P1 core가 M상태에서 다른 core의 데이터 read요청. : P1의 캐시 라인은 O, 요청한 캐시 라인은 S. P1의 캐시 라인을 요청 캐시 라인에 복사. 
- share 상태의 두 캐시 라인 중 하나가 폐기. : 그래도 독점상태인지 인지 불가 


**Owned state의 용도**는 해당 상태에 있는 cache의 데이터가 최신 상태임을 의미한다.
자신이 가장 최근에 해당 캐시 라인을 Modify 하였기 때문이다.
M 상태에서 다른 코어가 해당 데이터를 read 요청하면 M 상태의 코어는 O 상태가 되고
read 한 코어의 cache는 S 상태가 된다.
이때  **M 상태가 된 캐시 라인을 메모리에 store하지 않고 그 값을 read한 cache에 직접 보내준다.**
즉, memory access를 하지않는다. -> **매우 빠르다.**


## MESI, MOSI, MOESI Quiz

<iframe width="560" height="315" src="https://www.youtube.com/embed/Cy6mwfAew3o" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

아직 나도 풀어보지는 않았다. 하지만 필요할 때, 풀어보면 좋을 것 같아 올린다.
