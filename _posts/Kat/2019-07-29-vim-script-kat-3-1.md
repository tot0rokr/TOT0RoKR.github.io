---
title: "Vim script - KAT(3-1)"
date: 2019-07-29T14:55:00-09:00
last_modified_at: 2019-10-01T23:39:00-09:00
categories:
- Vim
tags:
- vim
- syntax
- vim script
- viml
excerpt: "Vim script(VimL) Syntax 문법"
---

## Intro

## vim 한글번역 문서

[![vim-koimage](https://user-images.githubusercontent.com/24751868/62033978-1ad34480-b228-11e9-9652-0e460942d17b.png)][vim-ko]

[Vim User Manual][vim-ko manual]


### Fold

[manual involving folding/Fold에 관련된 manual][vim-ko fold]을 살펴볼 수 있다.




## Scripting the Vim editor

This Chapter is refering on [Vim editor Tutorials][vim-edit-tuto]
이 카테고리는 [Vim editor Tutorials][vim-edit-tuto]를 바탕으로 작성되었습니다.

### vim version

``` sh
$ vim --version
```

You can see the installed version of vim, compiled option, usable modules  
**=** 설치된 vim에 대한 version과 compile 옵션, 사용할 수 있는 module을 볼 수 있다.


### Vimscript

You can read Vim's own documentation
``` vim
:help vim-script-intro
```

#### Running Vim script

``` vim
:source /full/path/to/the/scriptfile.vim
```

scriptfile.vim written vimscript is included within current vim session.  
**=** vim script를 현재 vim session에 포함한다.

``` vim
:call MyBackupFunc(argu1, argu2)
```

Run MyBackupFunc() within current vim session  
**=** 현재 vim session에 포함된 MyBackupFunc을 수행한다.


``` vim
:nmap ;s :source /full/path/to/the/scriptfile.vim<CR>
:nmap \b :call MyBackupFunc(argu1, argu2)<CR>
```

Mapped over statements to `;s` and `\b`  
**=** 위 명령을 `;s`와 `\b` 로 키매핑  

Generally, placed in `$HOME/.vimrc`  
`$HOME/.vimrc`에 위치해도 된다.


### Mapping

1. Type
    - nmap: **n**ormal-mode key **map**ping

1. Option
    - `<silent>`: Not to echo any command it's excecuting
    ``` vim
    :nmap <slient> ;s :call ToggleSomething()<CR>
    ```

1. Unprintable characters
    - `<CR>`: carriage return
    - `<Space>`: space
    - `<F1>` - `<F12>`: function key on keyboard
    - You can see other similar symbols
    ``` vim
    :help keycodes
    ```


### Vimscript statements

Run a statement across multiple lines with a single backslash:

``` vim
call Func(
\           argu1,
\           argu2,
\           argu3
\       )
```

Put two or more statements on a single line by separating them
with a vertical bar:

``` vim
echo "Starting..." | call Phase(1) | call Phase(2) | echo "Done" | "Comment
```


### Comments

Vimscript comments start with a double-quote and continue to the end of the line
``` vim
call Func(argu1, argu2) " This is comment of Func()
```

You can't put a comment anywhere that a string might be expected,
as `echo` command. So you can fix the above problem by using a vertical bar
to explicitly begin a new statement before starting the comment, like so:  
**=** `echo`와 같이 string으로 오해될 수 있는 곳에는 쌍따옴표만으로 comment를
사용할 수 없다. 그래서 comment를 시작하기 전에 vertical bar (`|`)를 이용해서
새 statement를 만들고(빈 statement) 그 곳에 comment를 작성한다. 다음과 같이:
``` vim
echo "hello~" | "Print hello
```


### Values and variables

Variable assignment requires a special keyword, `let`:
``` vim
let str = "String"
let int = 165
let list = ['A', 'B', 67, 'D', 69, ['a', 'b', 'c']]
let dict = {'key':'value', 'number':123, 'child':{'parent':'dict'}}
```

Strings can be specified with either double-quotes or single-quotes as delimiters.
- Double-quoted strings honor "escape sequences" such as "\n \t \u263A \\\<ESC\>"
- Single-quoted strings treat everthing as literal characters
except two consecutive single-quotes


#### Data Type
1. **scalar**: a single value, such as a string or a number
1. **list**: an ordered sequence of values delimited by square brackets,
with implicit integer indices starting at zero
1. **dictionary**: an unordered set of values delimited by braces,
with explicit string keys

Variables have no inherent type. Instead, they take on the type of the
first value assigned to them. Variable types, once assigned, are permanent
and strictly enforced at runtime.  
**=** 변수는 타입을 갖지 않는다. 대신, 처음 값을 할당한 것으로 타입을 정한다.
한 번 정해진 변수의 타입은 runtime 동안 영구적이고 엄격하게 강제한다.

#### Variable scope

By default, a variable is scoped to the function in witch it is first assigned to,
or is global if its first assignment occurs outside any function.  
**=** 기본적으로, 변수는 선언된 함수 내의 범위를 갖거나 함수 바깥에 선언되면 전역
을 범위로 갖는다.

However, variables may also be explicitly declared as belonging to other scopes,
using a variety of prefixes.
**=** 그렇지만, 변수는 또한 다양한 prefix를 이용해서 다른 scope에 소속하도록
명시적으로 선언될 수 있다.

|Prefix|Meaning|
|:-----|:------|
|**g:**varname|global|
|**s:**varname|local to the current script file|
|**w:**varname|local to the current editor window|
|**t:**varname|local to the current editor tab|
|**b:**varname|local to the current editor buffer|
|**l:**varname|local to the current function|
|**a:**varname|a parameter of the current function|
|**v:**varname|one that Vim predefines|


#### Pseudovariable

|Prefix|Meaning|
|:-----|:------|
|**&**varname|A Vim option(local option if defined, otherwise global)|
|**&l:**varname|A local Vim option|
|**&g:**varname|A global Vim option|
|**@**varname|A Vim register|
|**$**varname|An environment variable|

``` vim
nmap <silent> ]] :let &tabstop += 1<CR>
nmap <silent> [[ :let &tabstop -= &tabstop > 1 ? 1 : 0<CR>
```


### Expressions (Operator)

- String-concatenate-and-assign: `let var.=expr`
- String concatenateion: `str.str`

pass others


### Caveats

#### Logical caveats

- Only the numeric value zero is false in a boolean context
- Any non-zero numeric value is considered true  
**=** C와 마찬다지로 0이면 false, 이외에는 전부 true
- All the logical and comparison operators consistently return the value 1 for true  
**=** 논리식 혹은 비교 연산은 true에 대해서 1을 return 한다.
- When a string is used as a boolean, it is first converted to an integer,
strings including empty string will mostly evaluate as being false  
**=** string은 참/거짓으로 사용될 때, 정수로 변환하는데, 빈 문자열을 포함하여
거의 모든 문자열을 0으로 계산한다.
- Solution
``` vim
if empty(result_string)
    echo "No result"
endif
```

#### Comparator caveats

- Comparing string
``` vim
if "foo" == "FOO"       |" set ignorecase
    echom "vim is case insensitive"
elseif "foo" == "foo"   |" set noignorecase
    echom "vim is case sensitive"
endif
```
- Case sensitive
``` vim
if name ==? 'Batman'         |"Equality always case insensitive
    echo "I'm Batman"
elseif name <#'ee cummings'  |"Less‑than always case sensitive
    echo "the sky was can dy lu minous"
endif
```

#### Arithmetic caveats

- Vim supported only integer arithmetic until version 7.2  
**=** 7.2버전 밑의 vim은 정수 연산밖에 지원하지 않는다.
- Problem with integer arithmetic
``` vim
for filenum in range(filecount)
    echo (filenum / filecount * 100) . '% done'
    call process_file(filenum)
endfor
```
Always, Echo will do: `0% done` because of integer division.
So you can as though: `echo filecount / 100.0`


### Scripting in Insert mode

You can use the **imap** or **iabbrev** commands to set up key-mappings or
abbreviations that can be used while inserting text. For example:  
**=** **imap** 혹은 **iabbrev** 명령을 사용하여 키매핑 혹은 약어를 만들 수 있다.

``` vim
iabbrev <silent> CWD <C-R>=getcwd()<CR>
imap <silent> <C-C> <C-R>=string(eval(input("Calculate: ")))<CR>
```

If you write "CWD" in insert mode it is changed your current working directory.
And there is a simple calculator that can call by typing CTRL-C during text insertions.  
**=** insert mode에서 CWD를 입력하면 현재 작업 디렉토리로 문자열이 치환되고,
CTRL-C입력을 통해서 간이 계산기를 호출할 수 있다. (계산된 문자열이 입력된다.)

Just put the appropriate Vimscript expression or function call between an initial
`<C-R>=` (which tells Vim to insert the result of evaluating what follows)
and a final `<CR>` (which tells Vim to actually evaluate the preceding expression).  
**=** `<C-R>=`은 약어가 입력되면 따라오는 문자열을 vim이 입력한다.



### User-defined Function

#### Declaring functions

``` vim
function ExpurgateText (text)
    let expurgated_text = a:text

    for expletive in [ 'cagal', 'frak', 'gorram', 'mebs', 'zarking']
        let expurgated_text
        \   = substitute(expurgated_text, expletive, '[DELETED]', 'g')
    endfor

    return expurgated_text
endfunction
```

Vimscript functions always return a value, so if no **return** is specified,
the function automatically returns zero.  
**=** 함수는 항상 리턴값을 가지며, return을 명시하지 않았을 경우 0을 반환한다.

Function names in Vimscript must start with an uppercase letter:  
**=** 함수의 이름은 항상 대문자로 시작한다.


#### Scope

Same [Variable Scope][vim-script-variable-scope]


#### Redeclarable functions

Function declarations are runtime statements, so if script is loaded twice,
any functions will be executed twice. So its behavior is that a function
redeclares  
**=** 함수 정의는 runtime 상태이기에 script를 두 번 load하면 함수들은 두 번 실행 될
것이다. 그래서 이 행위는 함수를 재정의 하는 것이다.

Redeclaring a function is treated as a fatal error (to prevent collisions 
where two separate scripts accidentally declare functions of the same name).  
**=** 함수 재정의는 치명적 오류로 간주된다. (서로 다른 독립된 script에 우연히 같은
이름의 함수가 정의되어 생긴 충돌을 막기 위해.)

So you can make function to be able to redeclare with **function!**  
**=** 그래서 우리는 재정의 할 수 있는 함수를 **function!**을 이용해서 만들 수 있다.

``` vim
function! s:save_backup ()
    let b:backup_count = exists('b:backup_count') ? b:backup_count+1 : 1
    return writefile(getline(1,'$'), bufname('%') . '_' . b:backup_count)
endfunction
```

in which case the scoping already ensures that the function won’t
collide with one from another script.  
**=** 이 경우에 이미 다른 스크립트와 충돌 나지 않을 것을 보장한다.
(이미 존재했던 함수면 이전의 함수를 무시하게 된다.)


#### Calling functions

1. Using a functions's return value
    - let success = setline('.', ExpurgateText(getline('.')) )

1. Using a function without using its return value
    - call SaveBackup()


#### Parameter lists

You can specify up to 20 explicitly named parameters immediately 
after the declaration of the subroutine’s name.  
**=** 서브루틴의 이름 선언 후에 즉시 20개 이상의 인자를 명시할 수 있다.

Once specified, the corresponding argument values for the current call can be 
accessed within the function by prefixing an a: to the parameter name:  
**=** 현재 호출동안 인자 값이 일치하는 것은 인자 이름 앞에 prefix **a:**으로 함수안에서
접근될 수 있다.

``` vim
function PrintDetails(name, title, email)
    echo 'Name:   '  a:title  a:name
    echo 'Contact:'  a:email
endfunction
```

If you don’t know how many arguments a function may be given, you can specify a 
variadic parameter list, using an ellipsis **(...)** instead of named parameters.
Those values are collected into a single variable: and array named **a:000**
Individual arguments are also given positional parameter names: **a:1, a:2, a:3, etc.**
The number of arguments is available as **a:0.**  
**=** 만약 얼마나 많은 인자를 필요로 하는지 알 수 없다면, 인자 이름 대신에 생략부호
**(...)** 를 이용해서 가변 인자를 명시할 수 있다.
그 변수들은 하나의 변수로 모아진다. 그 배열의 이름은 **a:000**이다.
각각 변수는 인자 위치에 따라 이름이 주어진다. **a:1, a:2, a:3, etc..**
인자의 수는 **a:0**로 알 수 있다.

``` vim
function Average(...)
    let sum = 0.0

    for nextval in a:000"a:000 is the list of arguments
        let sum += nextval
    endfor

    return sum / a:0"a:0 is the number of arguments
endfunction
```

``` vim
function CommentBlock(comment, ...)
    "If 1 or more optional args, first optional arg is introducer...
    let introducer =  a:0 >= 1  ?  a:1  :  "//"

    "If 2 or more optional args, second optional arg is boxing character...
    let box_char   =  a:0 >= 2  ?  a:2  :  "*"

    "If 3 or more optional args, third optional arg is comment width...
    let width      =  a:0 >= 3  ?  a:3  :  strlen(a:comment) + 2

    " Build the comment box and put the comment inside it...
    return introducer . repeat(box_char,width) . "\<CR>"
    \    . introducer . " " . a:comment        . "\<CR>"
    \    . introducer . repeat(box_char,width) . "\<CR>"
endfunction
```


### Functions and line ranges

``` vim
"Delete every line from the current line (.) to the end-of-file ($)...
:.,$delete

"Replace "foo" with "bar" everywhere in lines 1 to 10
:1,10s/foo/bar/

"Center every line from five above the current line to five below it...
:-5,+5center
```
You can type :help cmdline-ranges in any Vim session to learn more about this facility.


If you called function which is doing something on current line:
``` vim
:call Function()
```

it would perform on current line only.
But if you specified a range before the `call`:
``` vim
:1,$call Function()
```


#### Internalizing function line ranges

The function is invoked only once, and two special arguments, a:firstline and
a:lastline, are set to the first and last line numbers in the range. If no range
is specified, both a:firstline and a:lastline are set to the current line number.  
**=** 함수는 한번에 적용된다. 그리고 두 특별한 인자는 range의 첫 번째와 마지막 라인 숫자가
지정된다(**a:firstline**, **a:lastline**). 만약 range가 명시되지 않으면,
**a:firstline**과 **a:lastline**은 현재 커서 라인 숫자로 지정된다.

``` vim
function DeAmperfyAll() range
    for linenum in range(a:firstline, a:lastline)
        "Replace loose ampersands (as in DeAmperfy())...
        let curr_line   = getline(linenum)
        let replacement = substitute(curr_line,'&\(\w\+;\)\@!','&','g')
        call setline(linenum, replacement)
    endfor

    "Report what was done...
    if a:lastline > a:firstline
        echo "DeAmperfied" (a:lastline - a:firstline + 1) "lines"
    endif
endfunction
```

``` vim
:1,$call DeAmperfyAll()
```

#### Visual ranges

You can make a visual block of text in visual-mode, and you can apply in there.
**=** visual block을 이용해서 위의 함수를 적용할 수도 있다.





[vim-ko]: http://vim-ko.github.io/ "vim-ko github page"
[vim-ko manual]: http://vim-ko.github.io/doc/usr_toc.html#usr_toc.txt
[vim-ko fold]: http://vim-ko.github.io/doc/usr_28.html#usr_28.txt

[vim-edit-tuto]: https://developer.ibm.com/articles/l-vim-script-1/

[vim-script-variable-scope]: https://tot0rokr.github.io/kat/vim/vim-script-kat-3-1/#variable-scope
