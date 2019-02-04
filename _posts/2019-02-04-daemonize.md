---
title: "Daemonize"
last_modified_at: 2019-02-04T11:15:00-09:00
categories:
- linux
tags:
- shell
- daemon
excerpt: "Reason for Daemonize of Program"
---

출처: <http://www.iamroot.org/xe/index.php?document_srl=202421&mid=Programming#2>

프로그램을 데몬화시키는 이유에 대한 포스팅이다.

문영일(문c)님의 답변을 그대로 옮겼는데, 좋은 내용인 것 같아서 포스팅으로 남긴다.

> 성능 또는 race condition을 고려해서 데모나이즈를 하는 것은 아닙니다.
> 쉘에서 백그라운드로 동작시키는 것과 데모나이즈화를 한 것의 차이는 다음 몇 가지 정도가 있습니다. 
> 1) 표준 입/출력 및 에러 file descriptor 사용 유무
>     - 데모나이즈화한 데몬들은 file descriptor 0, 1, 2번을 사용하지 않게 합니다.
> 2) 부모 태스크 상속 유무
>     - 데모나이즈화한 데몬들은 부모 상속 연결 고리를 끊어 없는 것처럼 만듭니다.
> 3) 시그널 공유 유무 
>     - 간단한 예로 telnet 로긴해서 백그라운드로 동작시킨 프로그램은 telnet session이 끊어질 때 sigint 및 sigpipe 등의 시그널을 공유받아 디폴트로 같이 중지하게 되어 있습니다. 
> 이미 아래 사이트에서 한 번 거론된 적이 있으므로 읽어보시기 바랍니다.
> <https://kldp.org/node/62759>
> <https://potatogim.net/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/%EB%8D%B0%EB%AA%A8%EB%82%98%EC%9D%B4%EC%A6%88>
> <http://software.clapper.org/daemonize/>


