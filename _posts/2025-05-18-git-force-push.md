---
title: "Git Smart Force Push: 더 안전하고 똑똑한 Force Push를 위한 gitconfig 활용"
last_modified_at: 2025-05-18T00:00:00-09:00
categories:
- Git
tags:
- push
excerpt: "Git Smart Force Push 패턴을 소개한다. 아래 alias는 사용자의 의도에 따라 remote, 대상 브랜치, refspec을 자동으로 판단해 `--force-with-lease`를 일관적으로 적용해준다."
---

`git push --force`는 강력하지만 위험한 명령이다. 협업 중인 브랜치에 잘못 사용하면 다른 사람의 커밋을 손실시키는 사고로 쉽게 이어질 수 있다. 그래서 많은 개발자들이 보다 안전한 대안인 `--force-with-lease`를 사용하지만, 매번 올바른 대상 브랜치(dst)를 지정해주는 것은 번거롭고 실수도 잦다.

이번 글에서는 이러한 문제를 해결하기 위해 `gitconfig`에 정의할 수 있는 **스마트한 force push alias**, 즉 _Git Smart Force Push_ 패턴을 소개한다. 아래 alias는 사용자의 의도에 따라 remote, 대상 브랜치, refspec을 자동으로 판단해 `--force-with-lease`를 일관적으로 적용해준다.

---

## 왜 Smart Force Push가 필요한가?

일반적인 force push는 다음과 같은 문제가 있다.

- 실수로 잘못된 브랜치를 덮어쓰기 쉽다
- lease 타깃을 명확히 지정하지 않으면 `--force-with-lease`도 기대만큼 안전하지 않다
- 업스트림 브랜치가 있는 경우와 없는 경우 처리 방식이 달라 매번 명령을 다르게 작성해야 한다

Smart Force Push alias는 이 모든 문제를 자동화해준다. 사용자는 단순히 `git pfl`만 입력하면 된다.

---

## Smart Force Push alias 소개

아래는 소개할 alias의 전체 코드다.

```sh
git config --global alias.pfl '!f() {
  set -e

  # 1) 기본값: 업스트림 추적 브랜치에서 remote/dst 가져오기
  if up=$(git rev-parse --abbrev-ref --symbolic-full-name @{u} 2>/dev/null); then
    remote=${up%%/*}
    default_dst=${up#*/}
  else
    # 업스트림 없으면: remote는 인자 1(없으면 origin), dst는 현재 브랜치
    remote=${1:-origin}
    default_dst=$(git rev-parse --abbrev-ref HEAD)
  fi

  # 2) 사용자가 refspec을 주면 그걸 사용, 아니면 dst만 밀기
  if [ $# -ge 2 ]; then
    refspec="$2"
    case "$refspec" in
      *:*) dst=${refspec##*:} ;;  # HEAD:dst 형태면 우측을 lease 대상으로
      *)   dst="$refspec" ;;
    esac
  else
    dst="$default_dst"
    refspec="$dst"
  fi

  exec git push --force-with-lease="$dst" "$remote" "$refspec"
}; f'
```

이 alias의 핵심은 **업스트림 추적 브랜치 정보를 기반으로 push 타깃을 자동 계산**하고, **항상 `--force-with-lease=<dst>`를 적용한다는 점**이다.

---

## 동작 방식 상세 설명

### 1) 업스트림 브랜치가 있으면 자동 활용

현재 브랜치가 `origin/main`처럼 업스트림을 추적하고 있는 경우:

- `remote` = `origin`
    
- `dst` = `main`
    

즉, 사용자가 별다른 인자를 주지 않아도 적절한 타깃으로 force-with-lease push가 수행된다.

### 2) 업스트림이 없는 경우 처리

일반적으로 feature 브랜치에서는 업스트림이 설정되지 않은 경우가 많다. 이때 alias는 다음과 같이 동작한다.

- `remote` = 첫 번째 인자(없으면 `origin`)
    
- `dst` = 현재 브랜치명
    

즉 다음과 같이 호출해도 자연스럽다.

```sh
git pfl
git pfl origin
```

### 3) 사용자가 refspec 제공 시 자동 해석

예를 들어:

```sh
git pfl origin HEAD:feature
```

이 경우:

- refspec = `HEAD:feature`
    
- lease 대상(dst) = `feature`
    

반대로 단일 브랜치명만 제공해도 OK:

```sh
git pfl origin my-branch
```

`my-branch`가 refspec이자 lease 대상이 된다.

---

## Smart Force Push가 제공하는 이점

### ✔ 더 적은 실수

lease 타깃을 명확히 지정하므로 협업 브랜치를 보호할 수 있다.

### ✔ 명령어 단순화

`git push origin HEAD:my-branch --force-with-lease=my-branch` 같은 긴 명령어를 더 이상 작성할 필요가 없다.

### ✔ 업스트림 기반 자동화

tracking 브랜치를 사용해 동작하므로 대부분의 상황에서 인자를 생략할 수 있다.

### ✔ 팀 내 안전한 워크플로우 구축

동료들과 함께 이 alias를 사용하면 모든 force push가 자동으로 lease 기반으로 제한되어 사고 가능성을 크게 줄일 수 있다.

---

## 실사용 예시

### 기본 push (업스트림 브랜치 기준)

```sh
git pfl
```

### 업스트림 없는 feature 브랜치에서 push

```sh
git pfl origin
```

### 명시적 refspec 제공

```sh
git pfl origin HEAD:experiment
```

### 특정 브랜치를 대상으로 push

```sh
git pfl origin release
```

---

## 마무리

Smart Force Push alias는 작은 설정이지만, 실수로 중요한 브랜치를 덮어쓰는 사고를 크게 줄여준다. 특히 협업 환경에서는 더 큰 효과를 발휘한다. Git 사용 경험이 쌓일수록 force push를 완전히 피하는 것은 어렵지만, 최소한 더 안전하고 명확한 방식으로 사용할 수는 있다.

개발 워크플로우의 안정성을 개선하고 싶다면 Git Smart Force Push 패턴을 적용해보는 것을 추천한다.
