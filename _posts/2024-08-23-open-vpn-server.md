---
title: "Build OpenVPN Server"
last_modified_at: 2024-08-23T00:00:00-09:00
categories:
- VPN
tags:
- open-vpn
- vpn
- server
excerpt: "Open VPN 서버를 구축하는 방법을 간략하게 알아본다. 또한 쉽고 간편하게 client를 추가 삭제하는 스크립트를 공개한다"
---

## 서버 구축

OpenVPN 서버를 docker 위에서 구축한다.

1. Ubuntu 20.04 이상을 서버에 설치
    1. AWS 인스턴스 등을 이용한다.
    1. 퍼블릭 IP 혹은 도메인
1. Docker 설치
    1. [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
1. 이미지 다운로드
    1. ```bash
        docker pull kylemanna/openvpn
        ```
1. 초기 설정
    1. ```bash
        export SERVER_DOMAIN=[SERVER_DOMAIN]
        export OVPN_DATA=/ovpn_data
        docker run -v $OVPN_DATA:/etc/openvpn --rm kylemanna/openvpn ovpn_genconfig -u "udp://$SERVER_DOMAIN" -N -d
        ```
    1. `[SERVER_DOMAIN]` 을 실제 도메인 이름으로 채운다
1. CA Certification과 Private Key를 생성한다.
    1. ```bash
        docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn ovpn_initpki
        ```
    1.  PassPhrase 를 입력하게 되는데, CA 인증 암호이므로 기억할 수 있는 암호를 설정한다.
        추후 진행 상황에서 PassPhrase 입력 요구시 해당 암호를 입력한다.
1. 서버 실행
    1. ```bash
        docker run -v $OVPN_DATA:/etc/openvpn -d -p 1194:1194/udp --name="ovpn" --restart="always" --cap-add=NET_ADMIN kylemanna/openvpn
        ```
1. 네트워크 방화벽 인바운드 설정에서 udp 1194번 포트를 연다.


## 클라이언트 구축

Docker 명령은 VPN이 설치된 서버에서 수행한다.

1. 클라이언트 설정
    1. ```bash
        docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn easyrsa build-client-full [CLIENT_NAME] nopass
        ```
    1. `[CLIENT_NAME]` 은 해당 클라이언트 이름을 설정한다. (클라이언트 별로 생성해야 한다.)
1. 클라이언트 설정 정보 생성
    1. ```bash
        docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn ovpn_getclient [CLIENT_NAME] > [CLIENT_NAME].ovpn
        ```
    1. 7위에서 설정한 `[CLIENT_NAME]` 을 입력한다.
    1. 해당 파일은 `/ovpn_data/pki/` 에 위치한다.
1. 생성된 `[CLIENT_NAME].ovpn` 파일을 클라이언트로 옮긴다.
    1. `scp` 등을 활용한다.
1. 클라이언트 머신에 OpenVPN을 설치한다. (또는, MAC OS X 등에서는 Tunnelblick 등의 프로그램을 사용한다.)
    1. ```bash
        sudo apt install openvpn
        ```
1. 클라이언트 머신에서 openvpn을 실행한다.
    1. ```bash
        sudo openvpn --config [CLIENT_NAME].ovpn
        ```

## 클라이언트 제거

1. 클라이언트 제거
    1. ```bash
        docker run -v $OVPN_DATA:/etc/openvpn --rm kylemanna/openvpn ovpn_revokeclient [CLIENT_NAME] remove
        ```
    1. `[CLIENT_NAME]` 제거할 클라이언트 이름을 입력한다.


## 간편 client 추가 삭제

아래 repository에서 사용할 수 있다. Pre-required 항목을 잘 수행한 뒤 사용할 수 있다.

https://github.com/tot0rokr/openvpn_adjust_client
