---
title: "systemd에서 특정 서비스의 실행 시점(ms 단위) 확인하기"
classes: "wide"
last_modified_at: 2022-08-22T00:00:00-09:00
categories:
- Linux
tags:
- systemd
- Linux
excerpt: "`systemd` 환경에서 특정 서비스가 부팅 후 언제 실행되었는지(ms 단위) 알고 싶을 때 그 방법을 단계별로 정리한 내용"
---

## 개요
`systemd` 환경에서 특정 서비스가 **부팅 후 언제 실행되었는지(ms 단위)** 알고 싶을 때는 `systemd-analyze`와 `systemctl show`를 조합해서 확인할 수 있다.  
아래는 그 방법을 단계별로 정리한 내용이다.

---

## 1. 서비스 실행 시각 기본 확인
```bash
systemctl show <서비스이름> -p ActiveEnterTimestamp
```

예시:

```
ActiveEnterTimestamp=Wed 2025-10-29 09:41:12 KST
```

→ 초 단위까지만 표시된다.

밀리초 단위로 보기 위해서는 다음 항목을 사용한다:

```bash
systemctl show <서비스이름> -p ActiveEnterTimestampMonotonic
```

출력 예시:

```
ActiveEnterTimestampMonotonic=1820345678
```

이 값은 **부팅 이후 경과한 시간(ns 단위)** 을 나타낸다.  
→ `1820345678 / 1_000_000 = 1820.345678 ms`

---

## 2. `systemd-analyze blame` 사용

```bash
systemd-analyze blame
```

각 서비스가 활성화되기까지 걸린 시간(ms 단위)을 표시한다.

예시:

```
5.732s  NetworkManager.service
1.234s  ssh.service
456ms   systemd-logind.service
  90ms  nginx.service
```

→ `nginx.service`는 실행 후 active 상태까지 90ms 걸렸다.  
단, **부팅 후 몇 초에 시작했는지**는 이 명령으로는 알 수 없다.

---

## 3. `systemd-analyze critical-chain` 사용

```bash
systemd-analyze critical-chain <서비스이름>
```

출력 예시:

```
graphical.target @2.013s
└─nginx.service @1.820s +192ms
```

- **1.820초**: 부팅 후 nginx 시작 시점
    
- **192ms**: active 상태까지 걸린 시간
    

따라서 nginx는 **부팅 후 1.820초에 실행 시작**,  
**2.013초에 완전히 활성화 완료**.

---

## 4. `journalctl`로 μs 단위 절대 시각 확인

```bash
journalctl -o short-precise -u <서비스이름> | grep "Started"
```

예시 출력:

```
Oct 29 09:41:12.345678 myhost systemd[1]: Started nginx.service.
```

여기 `09:41:12.345678`은 **μs 단위 절대 시각**이므로, 실제 ms 단위까지 정밀한 timestamp를 확인할 수 있다.

---

## 5. 정리표

|명령|용도|시간 기준|단위|
|---|---|---|---|
|`systemd-analyze blame`|서비스별 실행 소요시간|상대시간 (부팅 내 비교용)|ms|
|`systemd-analyze critical-chain <svc>`|부팅 시 타이밍 확인|부팅 후 시작 시점|ms (또는 s)|
|`systemctl show -p ActiveEnterTimestampMonotonic`|부팅 이후 경과 시간|나노초 (정확)||
|`journalctl -o short-precise`|실제 로그 시각 확인|절대시간|μs|

---

## 6. 추가: 수치 계산 예시

```bash
systemctl show nginx -p ActiveEnterTimestampMonotonic
```

```
ActiveEnterTimestampMonotonic=1820345678
```

나노초 단위를 ms로 변환:

```
1820345678 / 1_000_000 = 1820.345678 ms
```

→ nginx는 부팅 후 약 **1.820초**에 active 상태에 진입했다.

---

## 결론

- **정확한 부팅 후 시점(ms 단위)** → `systemd-analyze critical-chain <서비스>`
    
- **정확한 나노초 단위 값** → `systemctl show -p ActiveEnterTimestampMonotonic <서비스>`
    
- **절대 시각까지 필요하면** → `journalctl -o short-precise -u <서비스>`

