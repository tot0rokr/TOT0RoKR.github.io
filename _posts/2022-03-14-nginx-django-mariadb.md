---
title: "Web Server 간단히 만들기 (Nginx-Django-MariaDB)"
last_modified_at: 2022-03-14T00:00:00-09:00
categories:
- Web
tags:
- web
- nginx
- django
- mariadb
excerpt: "Nginx-Django-MariaDB"
---

## 초 스피드 Web 서버 뚝딱

### 선행조건

Docker 설치

```bash
$ sudo apt-get install docker.io
$ sudo usermod -aG docker {현재 사용자}
쉘 재접속
```

했는데도 /var/run/docker.sock: connect: permission denied가 뜨면
  ```bash
  $ sudo chmod 666 /var/run/docker.sock
  ```


### Docker 이미지 생성

#### Mariadb

```bash
$ docker pull mariadb
```

각 Dockerfile을 서로 다른 디렉토리에 넣고, build는 해당 디렉토리 위에서.

#### Django

```dockerfile
FROM python:3.10.2                  # 버전은 상관 무
RUN pip3 install django
VOLUME /app
WORKDIR /app

EXPOSE 8888

RUN pip3 install gunicorn
RUN pip3 install mysqlclient

# CMD sh -c "python3 manage.py migrate && python3 manage.py runserver 0.0.0.0:80"
CMD ["gunicorn", "--bind", "0.0.0.0:8888", "neo.wsgi:application"]
```

#### nginx

```dockerfile
FROM nginx:latest

VOLUME [/etc/nginx/conf.d]
VOLUME [/usr/share/nginx/app]

EXPOSE 8000
```

#### Build

```bash
$ docker build -t {이미지 이름} .
```


### Docker-compose로 컨테이너 실행

간단한 문법 및 명령어: https://darrengwon.tistory.com/793

#### docker-compose.yml 생성

```dockerfile
version: '3'

services:
  db:
    image: mariadb
    volumes:
      - "db-data:/var/lib/mysql"
    environment:
      - MARIADB_USER=${DB_USER}
      - MARIADB_PASSWORD=${DB_PASS}
      - MARIADB_ROOT_PASSWORD=${DB_ROOT_PASS}
    networks:
      - db-net
    restart: always

  web:
    image: {Django 이미지}
    volumes:
      - {Django App}:/app"
    environment:
      - DB_NAME=${DB_NAME}
      - DB_USER=${DB_USER}
      - DB_PASS=${DB_PASS}
      - DJANGO_SECRET_KEY=${DJANGO_SECRET_KEY}
      - DJANGO_ALLOWED_HOSTS=${DJANGO_ALLOWED_HOSTS}
    networks:
      - web-net
      - db-net
    depends_on:
      - db
    links:
      - "db:maria"
    restart: always

  nginx:
    image: {Nginx 이미지}
    volumes:
      - "{Nginx Site Configures}:/etc/nginx/conf.d"
      - "{Nginx Static Files}:/usr/share/nginx/app"
    ports:
      - "80:80"
    networks:
      - web-net
    depends_on:
      - web
    links:
      - "web:django"
    restart: always

networks:
  web-net:
  db-net:

volumes:
  db-data:
```

대충 이렇게 작성하면 된다.
환경변수는 대충 파일에다 때려넣으면 된다.

DJANGO\_SECRET\_KEY 설정 방법: https://wayhome25.github.io/django/2017/07/11/django-settings-secret-key/
 - Key 새로 생성: https://miniwebtool.com/django-secret-key-generator/


#### docker-compose 실행

```bash
$ docker-compose --env-file {환경변수 파일} config   # configuration 확인
$ docker-compose --env-file {환경변수 파일} up       # 실행
```

#### 첫 실행

1. MariaDB 컨테이너로 들어가 `$ mysql -p`. pw는 {DB\_ROOT\_PASS}
1. `grant all privileges on DB_NAME.* to '{DB_USER}'@'%'`
1. Django 컨테이너로 들어가 `$ cd /app`
1. `python3 manage.py startproject {Project Name} .`
1. `python3 manage.py startapp {App Name}`
1. `Project Name/setting.py`에서 DEBUG, ALLOWED\_FILE, DATABASES를 변경
1. Nginx 컨테이너로 들어가 `$ cd /etc/nginx/conf.d`
1. conf 파일 생성  
  ```conf
  upstream web {
      server django:8888;
  }

  server {
      listen 80;
      server_name localhost;

      location / {
          proxy_pass http://django/;
          proxy_redirect     off;
          proxy_set_header   Host $host;
          proxy_set_header   X-Real-IP $remote_addr;
          proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
      }

      location /static/ {
          alias /usr/share/nginx/app/intra/static/;
      }
  }
  ```

## Bug Report
|tag|error|해결방법|
|---|-----|--------|
|   |     |        |



## 사이트 공유
|tag|목적|링크|
|---|---|---|
|Django|가이드북|https://wikidocs.net/110801|
|Django|파이썬에서 환경 변수 읽어오기|https://www.daleseo.com/python-os-environ/|
|Django|Secret Key 생성|https://miniwebtool.com/django-secret-key-generator/|
|MariaDB|사용자 권한 설정 쿼리|https://tipland.tistory.com/47|
|MariaDB|쿼리 핸드북|http://www.tcpschool.com/mysql/mysql_basic_create|
|DockerCompose|간단한 문법과 명령어|https://darrengwon.tistory.com/793|
|DockerCompose|**공식** 문법|https://docs.docker.com/compose/compose-file/compose-file-v3/|
|DockerCompose|**해석** 문법|https://runebook.dev/ko/docs/docker/compose/compose-file/index|
|Docker|**공식** 명령어|https://docs.docker.com/engine/reference/commandline/run/|
|Docker|네트워크 연결|https://www.daleseo.com/docker-networks/|
|Docker|Dockerfile 문법|https://freedeveloper.tistory.com/188|



