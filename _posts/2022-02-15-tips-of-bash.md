---
title: "Tips of bash"
last_modified_at: 2022-02-15T00:00:00-09:00
categories:
- Shell
- Bash
tags:
- sh
excerpt: "Shell 정보"
---


## Shell 잘 쓰기

~~나는 고집불통 정통 bash 유저다. zsh? 그딴 무거운 툴 쓸거면 vim 쓰지도 않았다.
Bash여 영원하라.~~


### History

#### HISTCONTROL

1. ignorespace: 명령 실행 시 처음 space가 포함되면 로그에 기록하지 않음
1. ignoredups: 명령이 연속으로 중복되면 무시
1. ignoreboth: 위 두개
1. erasedups: 중복 로그는 삭제하고 최신로그만 기록

```
export HISTCONTROL=ignoreboth:erasedups
```

#### HISTIGNORE

로그에 기록하지 않는 명령 리스트. `:`로 구분한다.

```
export HISTIGNORE="pwd:ls:ll:l.:ll.:la:lla"
```


### Prompt

#### PROMPT\_COMMAND

bash가 prompt를 표시하기 직전에 실행하는 bash 명령어

```
export PROMPT_COMMAND="echo \"==============================================================================\""
export PROMPT_COMMAND="str="="; for ((i=1; i<$COLUMNS; i++)); do str="${str}="; done; echo $str"
```



### 반복문

#### for

```
for {변수} in {리스트 | 이터레이션}
do
    {명령어}
done

or

for ((i=0; i<{식}; {식}))
do
    {명령어}
done
```
