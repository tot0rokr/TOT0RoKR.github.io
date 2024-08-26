---
title: "My First Open-source Project Contribution with Zephyr RTOS"
last_modified_at: 2024-08-26T00:00:00-09:00
categories:
- Open-source
tags:
- zephyr
- open-source
- git
- github
excerpt: "대규모 오픈소스 기여에 대한 첫 경험(므흣)"
---

~~↓↓↓↓일단 뱃지 자랑부터↓↓↓↓~~

<div data-iframe-width="300" data-iframe-height="300" data-share-badge-id="298b7d3a-ec22-4030-8751-8963c016feec" data-share-badge-host="https://www.credly.com"></div><script type="text/javascript" async src="//cdn.credly.com/assets/utilities/embed.js"></script>

[Zephyr](https://zephyrproject.org/)라는 대형 오픈소스 RTOS 프로젝트에 기여를 해보았다. 이전까지는
소규모 오픈소스에서 문서 수정같은 자잘한 PR은 올려봤지만 대형 오픈소스 커뮤니티에 참여하는
것은 처음이었다. Bluetooth
mesh 파트에서 치명적인 버그를 발견해서 패치해서 사용하다가 문득 PR을 보내봐도 되지 않을까 싶어
시작했다. Linux Kernel 같은 경우에는 최신 커널을 사용하지 않아 버그를 발견해도 최신 커밋에 오면 결국
리팩토링 되었거나 버그 패치가 이루어진 이후였기 때문에 마땅히 기회가 없었다. 하지만 Bluetooth mesh는
표준 스펙으로 지정된지 얼마 되지 않았고 심지어 패치를 수행한 BLOB Transfer 같은 경우에는 스펙문서가
나온지 1년도 채 되지 않았기 때문에 여지가 있어보였다(물론 Draft 버전은 1년이 넘었고 Zephyr는 활발히
PR이 올라오는 편이라 확실하진 않았다).

해당 PR은 [zephyrproject-rtos/zephyr#77315](https://github.com/zephyrproject-rtos/zephyr/pull/77315) 여기서 확인할 수 있다.

내가 수정한 부분은 [Bluetooth Mesh BLOB Transfer](https://www.bluetooth.com/specifications/specs/mesh-binary-large-object-transfer-model/)
과정에서 중간에 Cancel할 시 특정 자료구조를 초기화하지 않는 버그였다. 나는 실제로 이 코드를 사용하던
유저이기 때문에 실사용 중에 발견한 문제라서 고칠 수 있었는데, 내 생각엔 이 코드 아직 아무도 사용하지
않는 것 같다. 혹은 많이 사용하지 않아 테스트가 적었고, 문제가 발생했어도 리셋으로 해결할 수 있어서
아무도 고치지 않았던 게 아닐까. 일단 안정화 되어있지 않은 점이나 자잘하게 고쳐야할 부분이 보이기도
한다. 추후 계속 모니터링 하다가 후속 PR도 보내볼 예정이다.

Zephyr 프로젝트는 [nrfconnect](https://github.com/nrfconnect)에서 fork한 프로젝트가 있는데 사실 나는
이쪽을 사용 중이었다. 때문에 이쪽에도 PR([nrfconnect/sdk-zephyr#1960](https://github.com/nrfconnect/sdk-zephyr/pull/1960))
을 올렸다. 그런데 업스트림 저장소에 올린 PR을 올리기 위해선 몇 가지 규칙이 있었는지 ~~하나의 PR을 더
올릴 기회를 날렸다!~~ 친절히 리뷰어가 설명해주었다.

cherry-pick을 하면서 오리지널 커밋 해시를 오리지널 해시에 적어줘야 했다. 직접 추가하면 해시의 일부만
추가하는 불상사가 생기니 `git cherry-pick -x --edit <commit>`을 통해 cherry-pick을 하는 방법을
사용하자. 오리지널 커밋을 `git push -f`를 통해 PR에 올린 커밋을 변경했다면 해당 해시를 적은 커밋
메시지도 수정해야함을 잊지 말자(이것 때문에 오랬동안 PR이 머지되지 못했다).

Zephyr PR이 merge되고 위 뱃지를 얻었다. 생각보다 오픈소스 기여하기도 쉽고 재미있었다.
