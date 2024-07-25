---
title: "Nrf Connect SDK based Bluetooth Mesh Firmware Expreiments"
last_modified_at: 2024-07-25T00:00:00-09:00
categories:
- blog
tags:
- blog
excerpt: "Nordic사에서 개발한 bluetooth mesh firmware 사용 중 벌어진 일"
---


## 환경

- Board: Nordic nrf52840 DK
- SDK: nrf Connect 2.6.0

## Transport layer 로그

### Replay 로그

`<wrn> bt_mesh_transport: Replay: src 0x7803 dst 0xd000 seq 0x5697d4`

동일 노드로부터 발생한 메시지가 이미 수신했던 패킷보다 낮은 시퀀스 번호를 갖는 경우에 발생. 해당
패킷은 처리하지 않고 무시(Ingore). 송신자의 메시지 재전송 옵션인 `network transmission interval` 혹은
`network transmission count` 를 조절하거나 메시지 사이의 송신 간격을 조절하여 해결할 수 있다. 주로
Segmented Message를 보낼 때, 세그먼트된 패킷이 많으면 보낼 패킷이 많아 전송 시간이 길어지면서 다음
메시지 이후에 패킷이 발행되거나 멀리 돌아 도달하는 경우에 발생한다.


### Ignoring old SeqAuth 로그

`<wrn> bt_mesh_transport: Ignoring old SeqAuth`

동일 노드로부터 발행한 segmented message가 최근 받고 있는 메시지보다 **낮은** sequence 번호를 갖는
패킷이 들어온 경우에 해당 패킷을 무시. `SeqAuth`로부터 시퀀스 번호를 추출하여 어떤 패킷이 최신에
발행된 메시지를 갖는 지 확인할 수 있다. Replay로그와 다른 점은, 메시지를 전부 수신한 게 아니라
segmented packet을 받는 도중에 오래된 시퀀스를 갖는 패킷이 들어온 경우에 발생한다. 해결방법은 Replay
로그와 동일하다.


### Duplicated SDU 로그

`<wrn> bt_mesh_transport: Duplicate SDU from src 0x7803`

동일 노드로부터 발행한 segmented message가 최근 받고 있는 메시지보다 **높은** 시퀀스 번호를 갖는
패킷이 들어온 경우에 먼저 받고 있던 메시지의 패킷들을 버림. Segmented message에 대한 세그먼트된
패킷을 아직 전부 수신하지 못한 상황에서 새로운 메시지의 세그먼트된 패킷을 수신한 경우에 먼저 받고
있던 패킷은 오래된 시퀀스를 갖는 패킷으로 간주해버리는 것이다. 앞전 메시지의 모든 세그먼트된 패킷을
채 다 받기도 전에 새로운 메시지를 발행한 것이므로 메시지 발행 간격을 늘려버리는 것으로 해결할 수
있다.


### SAR Discard timeout expired 로그

`<wrn> bt_mesh_transport: SAR Discard timeout expired`

Segmented message를 수신하기위한 timer가 만료될때 발생한다. Timer가 만료되기 전까지 해당 메시지의
모든 세그먼트된 패킷을 수신하지 못했다는 뜻이므로, 네트워크 상태가 좋지 않아 메시지가 많이 누락되거나
segmentation이 너무 많이 되어있을 수도 있고, `network transmission count`가 낮아 문제가 생길 수도
있다.
