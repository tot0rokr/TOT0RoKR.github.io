---
title: "Sharing Storage by Linux on Hyper-V"
last_modified_at: 2019-07-25T01:39:00-09:00
categories:
- Hyper-v
tags:
- hyper-v
- sharing
excerpt: "Hyper-V에서 host인 Windows와 guest인 Linux 간의 디렉터리 공유"
---

## Sharing Storage

Windows 10 Pro를 이용하면 운영체제에서 제공하는 하이퍼바이저인
Hyper-V 기능이 존재한다.

필자는 이 하이퍼바이저를 이용해서 Linux 서버를 구동하고, 모든 리눅스 작업은
여기서 진행한다.

그렇기 때문에 Host OS인 Window 10 Pro와 Guest OS인 Linux 간에 데이터 이동이
원활하게 이루어져야 했고, 가장 간단하게 수행 가능한 방법이 Windows의 공유폴더를
이용해 리눅스에서 CIFS로 mount하여 사용하는 것이 가장 편리하고 깔끔했다.


## How to Use

### 1. Windows에서 공유 디렉토리를 생성한다.

새 폴더를 만든 뒤 적절한 이름으로 변경한다.

![new directory](https://user-images.githubusercontent.com/24751868/61812150-e6553680-ae7d-11e9-86fd-a4836406d41f.png)


### 2. Windows 공유 디렉토리로 변경

##### (1) 생성한 디렉토리를 우측클릭하면 보이는 속성을 클릭 후 상단에 보이는 공유 탭으로
이동한다.

![attribute sharing](https://user-images.githubusercontent.com/24751868/61812221-07b62280-ae7e-11e9-9d23-3c973aa8df55.png)

##### (2) 파란색 박스로 하이라이트 되어진 `공유(S)...`를 클릭한다.

![with user](https://user-images.githubusercontent.com/24751868/61812294-2ddbc280-ae7e-11e9-8daa-8a0561fe9847.png)

##### (3) 사용자 이름을 확인하고, password를 숙지한 후 방패 ~~_넌 못지나간다._~~ 공유(H)
를 클릭한다. 보안창이 뜨면 허용해준다.


### 3. Linux에서 공유 디렉토리 Mount

##### (1) CIFS 을 사용하기 위한 설치.

``` sh
sudo apt-get install -y cifs-utils
```

##### (2) 공유 디렉토리를 CIFS 파일시스템으로 mount해준다.

``` sh
$ sudo mount //{host_ip_address}/{shared_directory} /mnt -t cifs -o username={username},password={password},noperm,uid=nobody,gid=nogroup,iocharset=utf8
```

위 명령을 수행한다. root 권한이 필요하므로 sudo를 이용했다.

- sudo: mount는 root 권한이 필요하다.
- {host_ip_address}: Host OS인 Windows의 ip 주소를 입력한다.
  - 윈도우에서 `Win + R` 단축키를 이용해서 실행창을 연다.
  - `cmd`를 입력한다.
  - `> ipconfig`를 입력한다.

![ip](https://user-images.githubusercontent.com/24751868/61814825-e22c1780-ae83-11e9-8b0f-50297f86b4ff.png)

- {shared_directory}: 큰 목차 1번에서 생성한 디렉터리 이름.
- cifs: cifs 사용
- {username}: Host OS의 계정 이름.
- {password}: {username}의 패스워드.
- uid=nobody: 누구나 접근할 수 있도록 권한을 설정한다.
- gid=nogroup: 위와 동일한 이유.
- iocharset=utf8: 인코딩 utf8.



### 4. 시나리오

##### (1) 아무것도 없는 상태에서 디렉터리 생성.
 
![write](https://user-images.githubusercontent.com/24751868/61813591-06d2c000-ae81-11e9-848f-8be375c04e50.png)


##### (2) Windows에서 Linux에서 생성한 디렉터리 확인 및 파일 삽입.

![ico](https://user-images.githubusercontent.com/24751868/61815220-b9f0e880-ae84-11e9-98e8-b7c6b449b829.png)


##### (3) Linux에서 파일 확인 및 사용.

![read](https://user-images.githubusercontent.com/24751868/61813547-e440a700-ae80-11e9-9d96-10cbb6a0945d.png)
