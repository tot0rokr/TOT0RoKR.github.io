---
title: "Develop Vim Plugin in Python - KAT(3-2)"
last_modified_at: 2019-07-29T20:16:00-09:00
categories:
- Vim
tags:
- vim
- plugin
- python
excerpt: "Python을 이용한 Vim Plugin 작성법"
---

## Introduce

Vim Script라고 불리는 Vim 전용 DSL인 VimL을 사용하여 플러그인을 개발할 수 있다.
그러나 제한적인 문법으로 인해 이 프로젝트에 적합하지 않은 언어로 판단하여
Python3를 이용하기로 하였다.

이 Post는

> [**Writing Vim plugin in Python**][WVPP]

> [**Creating VIM plugin with Python**][CVPP]

의 많은 부분 참고하였다. 추후 많은 분들이 따라할 수 있도록 원본 글의 내용을
최대한 유지한 채 본 글을 작성하였다. 단, python2 기준으로 작성된 부분은
모두 python3를 기준으로 변경하였다.

### Vim Python Support

Vim이 Python으로 작성된 플러그인을 수행하기 위해선 설치된 Vim이 Python을
지원하는지 확인해야 한다.

``` sh
$ vim --version
```

위 명령어를 수행했을 때, `+python`이 있을 시엔 Python2를 지원하고
`+python3`가 있을 시엔 Python3를 지원하는 것이다.

저의 경우엔 Python3로 개발할 것이고, 마침 vim도 Python3를 지원하므로
이 문서는 Python3 개발을 기준으로 작성할 것이다.


## Usage


### Plugin structure

플러그인 디렉터리 내부:

```
{% raw %}
sampleplugin/
├ doc/
│   └ sampleplugin.doc
├ plugin/
│  └ sampleplugin.vim
├ LICENSE
└ README
{% endraw %}
```

### Plugin Import

1. **sampleplugin.vim**에 Plugin으로 사용할 내용을 작성.
2. `~/.vim/bundle/`에 위 프로젝트를 `ln -s` 혹은 `mv` 함.
3. `~/.vimrc`에 다음과 같이 작성함.
``` vim
Plugin 'file:///home/{username}/.vim/bundle/sampleplugin'
```
4. vim 재실행.


### Use Python3

**`.vim` 파일에서 python 사용. `sampleplugin.vim`:**

{% highlight vim linenos=table %}
if !has('python3')
    echo "Error: Required vim compiled with +python3"
    finish
endif

python3 << EOF
print ("Hello from Vim's Python!")
EOF
{% endhighlight %}


**python 파일을 import하여 사용. `sampleplugin.vim`:**


{% highlight vim linenos=table %}
let s:plugin_root_dir = fnamemodify(resolve(expand('<sfile>:p')), ':h')

python3 << EOF
import sys
from os.path import normpath, join
import vim
plugin_root_dir = vim.eval('s:plugin_root_dir')
python_root_dir = normpath(join(plugin_root_dir, '..', 'python3'))
sys.path.insert(0, python_root_dir)
import sample
EOF
{% endhighlight %}

- 1: 플러그인 디렉터리 경로를 지역변수에 저장
- 7: python script에서 지역변수에 접근
- 8: python 코드가 있는 디렉터리 경로 구축
- 9: python 코드가 있는 디렉터리 경로를 sys.path에 추가
- 10: 우리가 작성할 파이썬 모듈을 import

`~/.vim/bundle`:

``` sh
$ mkdir sampleplugin/python3
$ touch sampleplugin/python3/sample.py
```

`~/.vim/bundle/sampleplugin/python3/sample.py`:

``` python
print "Hello from Python source code!"

def print_test():
    print ("Hello from Python Function \'print_test\'")
```

`~/.vim/bundle/sampleplugin/plugin/sampleplugin.vim`:

``` vim
function! Sample()
    python3 print("asd")
    python3 sample.print_test()
endfunction
```

Plugin 함수 수행

``` vim
: call Sample()
```

![SampleFunc](https://user-images.githubusercontent.com/24751868/62057815-4c193800-b25b-11e9-829e-b88fab1cb4d2.png)


### Vim Scripting through Python

[Vim Scripting through Python](http://heather.cs.ucdavis.edu/~matloff/Python/PyVimscript.html)

[nvim help](https://neovim.io/doc/user/if_pyth.html)

[vim help](http://vimdoc.sourceforge.net/htmldoc/if_pyth.html)



[WVPP]: http://candidtim.github.io/vim/2017/08/11/write-vim-plugin-in-python.html
[CVPP]: https://www.thekerneltrip.com/ocaml/vim-ocaml-plugin/
