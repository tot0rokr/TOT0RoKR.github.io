---
title: "build_all_zonelists()"
classes: wide
excerpt: "UP 되어 있는 모든 node와 zone에 대해 zonelist를 생성한다."
date: 2019-02-08T11:52:00-09:00
last_modified_at: 2019-02-15T04:08:00-09:00
tag:
- zonelist
- fallback
- page
- numa
- node
---

## Intro

### Zonelist

메모리 할당을 요청할 때, 특정 zone에 대해 할당을 요청한다.
그러나 해당 zone에 요청한 size 만큼의 공간이 존재하지 않을 때, 다른 zone에서 공간을 할당 받아야 한다.
이 것을 **Fallback** 이라고 하며, 할당 요청한 zone이 아닌 다른 zone에서 공간을 할당받는다.
이 때, 이 **fallback**할 zone을 선택하는 기법으로 **zonelist* 기법을 사용한다.

**zonelist**는 **fallback** 발생 시 대신 할당해 줄 zone의 list를 말하는 것인데,
처리할 cpu에서 접근하기 용이한 zone을 선택해서 순서를 정한다.

이 순서는 다음과 같은 가중치로 판단한다.

1. **NUMA** 시스템에서는 **Node**라는 메모리 그룹을 사용하는데, 이 CPU가 속한 Node에서 다른 Node의 메모리를
접근하려면 **distance**에 비례해서 Load/Store 시간이 추가적으로 걸리게 된다. 즉, 가까운 Node가 fallback하기 좋다.
2. CPU가 없는 Node. 즉, 메모리만으로 구성된 Node(SoC 등)가 존재하면, 아직 CPU에 의해 사용되지 않는 메모리이므로
fallback하기 좋은 조건이다.
3. 다른 Node들에 대해 비슷한 같은 거리를 같는 Node들이 존재하면 한 Node에 fallback이 쏠릴 수 있다.
그러므로, RoundRobin 기법을 이용해, 같은 거리, 같은 조건의 Node에 대해서 zonelist 순서를 골고루 분산시킨다. (영상에 과정 참조)
4. 완벽하게 동일한 조건이면, zonelist를 생성하는 node보다 번호가 더 큰 node를 우선으로 한다.

또한, **no-fallback** zonelists 이라는 것도 존재하며, 이는 fallback하지 않는 zonelist를 의미한다.
fallback을 사용하지 않을 **task**에 대해 지정한다.

build_all_zonelists() 함수에서는 위 zonelist를 각 cpu별로 초기화 해준다.

**Memory HotPlug** 시에도 zonelists를 수정하는 것으로 파악된다. (당연하다)


## 동작 과정

{% include video id="nhxY_XhtJzQ" provider="youtube" %} 
