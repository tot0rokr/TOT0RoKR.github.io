---
title: "Vim Easily Remove Swap File"
last_modified_at: 2019-10-08T00:00:00-09:00
categories:
- Vim
tags:
- vim
excerpt: "(KR|ENG) Vim easily remove swap file. 빔 쉽게 swap 파일을 지우기"
---


First, You should set `set dir={somepath}` in `~/.vimrc`, swap files are
located in `{somepath}`. `{somepath}` is set where you want.  
**=** 먼저, swap file이 생성될 디렉터리 경로인 `{somepath}`을 정하고,
`~/.vimrc`에 `set dir={somepath}`를 추가한다.

``` vim
set dir=~/.vim/temp
```


And, Append a function as follow in `~/.vimrc`  
**=** 그리고, `~/.vimrc`에 아래의 함수를 추가한다.

``` vim
function! DeleteSwap()
    exec('! rm ' . &dir . '/' . @% . '.swp')
endfunction
```


Finally, You can call above function in a file which is notified of existing swap
file by vim.  
**=** 마지막으로, vim으로부터 swap 파일이 존재한다는 알림을 받은 파일에서 함수를
호출 할 수 있다.

``` vim
call Deleteswap()
```


