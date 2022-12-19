---
title: "Python co-operation tools"
last_modified_at: 2022-08-11T00:00:00-09:00
categories:
- Contribute
tags:
- contribute
- cooperation
- python
- tools
excerpt: "Python tools for co-operation"
---

# pre-commit

git commit 사용 전에 발동하는 hooking tool. commit 시 coding style을 통일하거나,
linter 실행을 위해 사용.

## install

```bash
$ pip install pre-commit # python이 있으면
```

## Usage

### 설정파일 생성

```bash
pre-commit sample-config > .pre-commit-config.yaml
```

### 기본 설정

```yaml
# See https://pre-commit.com for more information
# See https://pre-commit.com/hooks.html for more hooks
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v3.2.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-added-large-files
```

- trailing-whitespace: 불필요한 공백 제거
- end-of-file-fixer: 파일 끝 개행 제거
- check-yaml: yaml 문법 체크
- check-added-large-files: 큰 파일 add 체크
  - github 등의 경우 대용량 파일을 업로드 할 수 없음
  - git-lfs 사용


### 실행

```bash
$ pre-commit run
```

**staging area**에 있는 파일들에 대하여 체크를 진행,
자동으로 hook 프로그램 실행.

### 자동화

```bash
$ pre-commit install
```

git commit 수행 시 자동으로 동작시켜줌.

![image](https://user-images.githubusercontent.com/24751868/184089311-1447daa3-9347-4343-9927-a2ddf98b756a.png)

### 업데이트

```bash
$ pre-commit autoupdate
```

hook repository의 버전 업데이트


# Black

코드 포맷터. 개발자들간에 서로 다른 코드 포맷을 거부하고, 일관성 있게 변경하는
도구.

## Install

```bash
$ pip install black
```

## Usage

```bash
$ black {FILENAME}
```

### Options

- `--check`: 실제로 변경하기 싫고, check만 하고 싶을 때 사용

### pre-commit 설정

```yaml
repos:
  - repo: https://github.com/psf/black
    rev: stable
    hooks:
      - id: black
```


# Pylint

Python 코드의 에러를 확인하고, 표준을 적용시키는 도구.
코드에서 구릿구릿한 냄새가 나면 지적질 해주고, 꼬라지를 점수로 평가한다.

## Usage

```bash
$ pylint {FILENAME}
```

### Options

`.pylintrc`에 옵션을 추가할 수 있음.

```bash
$ pylint --generate-rcfile > .pylintrc
```

rc파일을 생성함. 옵션을 커스터마이징 할 수 있음.
옵션 내용은 [여기서][pylint_link] 확인.

[pylint_link]: https://pylint.pycqa.org/en/latest/user_guide/configuration/all-options.html



### pre-commit 설정

```yaml
repos:
  - repo: local
    hooks:
      - id: pylint
        name: pylint
        entry: pylint
        language: system
        types: [python]
        require_serial: true
```

원격 repo에 있는 pylint는 로컬 라이브러리(패키지)에 접근할 수 없어서
import 에러가 발생. 때문에, pylint를 로컬에 설치하고, 로컬 pylint를
pre-commit에 설정해주는 방식으로 사용해야 함.



# flake8

python 코드 체크 툴. 다음과 같은 것들로 이루어져 있다.
- PyFlakes: 코드의 에러 체크(pyflake)
- pycodestyle: PEP8에 준거하고 있는지를 체크(pycodestyle)
- Ned Batchelder's McCabe Script: 순환 복잡도를 체크(mccabe)


## Usage

```bash
$ flake8 {FILENAME}
```

### Ignoring Error

- `# noqa: {error[,error...]}`: 해당 라인을 스킵
- `# flake8: noqa`: 해당 파일 전체를 스킵


### pre-commit 설정

```yaml
repos:
  - repo: https://github.com/PyCQA/flake8
    rev: 5.0.4
    hooks:
      - id: flake8
```


# isort

import 패키지 순서를 맞춰줌. 표준 패키지, 서브파티 패키지, 사용자 패키지 순서
및 알파벳 순서.

## Usage

```bash
$ isort {FILENAME}
```

### Skip

- `# isort:skip`: 해당 라인을 스킵
- `""" isort:skip_file """`: module doc string에 삽입 시 파일 전체를 스킵

### pre-commit 설정

```yaml
repos:
  - repo: https://github.com/PyCQA/isort
    rev: 5.10.1
    hooks:
      - id: isort
```


# mypy

Static Type Checker. 일반적으로 typing 라이브러리와 함께 사용한다.

https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html

vim 플러그인도 있음.

## Usage

```bash
$ mypy {FILENAME}
```

### Ignoring

- `# type: ignore`: import 패키지의 타입체크 스킵

### pre-commit 설정

```yaml
repos:
  - repo: local
    hooks:
      - id: mypy
        name: mypy
        entry: mypy
        language: system
        types: [python]
        require_serial: true
```

mypy 또한 외부 패키지를 이용하므로, 설치된 로컬 패키지를 접근하기 위해,
원격이 아닌 로컬의 mypy를 사용해야한다.
