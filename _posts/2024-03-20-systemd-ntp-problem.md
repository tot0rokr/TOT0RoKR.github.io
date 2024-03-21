---
title: "NTP daemon blocks systemd bootup process"
last_modified_at: 2024-03-20T04:14:00-09:00
categories:
- Systemd
tags:
- systemd
- systemd-timesyncd
- ntp
- linux
- debian
- tinkerboard
excerpt: "NTP daemon blocks systemd-time-wait-sync"
---

## Colision between timesyncd and ntpd

원인은 알 수 없지만 systemd의 NTP 데몬인 `systemd-timesyncd.service`와 `ntp.service`를 함께
사용하면, 부팅 과정에서 실행 되어야할 `systemd-time-wait-sync.service`가 중단되고 이후 처리되는
`timers.target`을 비롯한 타이머 기반 서비스가 모두 block된다. 특징은 `systemctl start BLAHBLAH`로
실행해도 아무 출력도, 아무 로그도 남기지 않은 채 무지성 대기를 한다는 점이다.

부득이하게 두 서비스 모두를 사용 해야한다면 아래링크에서 답을 찾을 수 있다.

- https://github.com/systemd/systemd/issues/14061

참고

- https://bugs.launchpad.net/ubuntu/+source/systemd/+bug/1937238
- https://github.com/systemd/systemd/issues/8683


## systemd-timesyncd

따라서 `ntpd` 대신 `systemd-timesyncd`를 사용할 수 있다. 아래 명령들로 시간을 확인하고 상태를 체크할
수 있다.

```
timedatectl status
timedatectl show
timedatectl show-timesync
timedatectl timesync-status
```
