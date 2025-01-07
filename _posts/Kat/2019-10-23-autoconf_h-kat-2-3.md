---
title: ".config and include/generated/autoconf.h - KAT(4-2)"
last_modified_at: 2019-10-23T15:44:00-09:00
categories:
- Config
tags:
- autoconf
- config
excerpt: "autoconf.h가 무엇이고 언제 만들어지는가?"
---

## What is the autoconf.h?

The **autoconf.h** is in **include/generated/** if your `cwd` is root directory
of kernel source.
It consist of C macro definitions like `#define CONFIG_SOMETHING 1`.
You can find this identifier where is in the `.config`.  
**=** **autoconf.h**는 커널 디렉토리 밑의 **include/generated/**에서 볼 수 있다.
이것은 `#define CONFIG_SOMETHING 1`과 같은 C 매크로 정의로 이루어져 있다.
또한 이 식별자들을 `.config`에서 찾을 수 있다.

`.config` is made from **Kconfigs** or **arch/$(ARCH)/defconfig** or
**arch/$(ARCH)/configs/defconfig** by doing as follows.  
**=** `.config`는 다음과 같은 행동을 통해 **Kconfig**들이나
**arch/$(ARCH)/defconfig**, **arch/$(ARCH)/configs/defconfig**으로부터 만들어진다.

``` sh
$ make defconfig
$ make ARCH=$(ARCH) defconfig
$ make menuconfig
$ make ARCH=$(ARCH) menuconfig
etc..
```

If you change kernel config for compiling kernel source through the above command,
`.config` is changed to it.
Identifier seen in menuconfig is added prefix **CONFIG\_**.  
**=** 커널 컴파일을 위해 커널 설정을 위와 같은 명령을 이용해서 바꾼다면,
`.config` 파일이 바뀌게 된다.
또한, 식별자의 앞에 **CONFIG\_**가 붙는다.


## When is the autoconf.h made?

You've already make `.config`, You can do command as follows.  
**=** `.config`를 만들었다면, 다음과 같은 명령을 수행할 수 있다.

``` sh
$ make
$ make ARCH=$(ARCH)
```

It is to compile Kernel source using `.config`.
Command `make` make **include/generated/autoconf.h** first. It is important in
kernel source because it is global options.
**=** `.config`파일을 이용해서 커널 소스를 컴파일한다.
명령어 `make`는 **include/generated/autoconf.h**를 먼저 만든다. 이 파일은
커널 소스에서 전역 옵션이기 떄문에 중요하다.


## Contents of autoconf.h

If a identifier called `SOMETHING` exist, a definitions is in **autoconf.h** as follows  
**=** `SOMETHING`이라는 식별자가 존재한다면 **autoconf.h**에는 다음과 같이
정의된다.

1. A config is get value of yes(`y`)
    ``` c
    #define CONFIG_SOMETHING 1
    ```
1. A config is get value of module(`m`)
    ``` c
    #define CONFIG_SOMETHING_MODULE 1
    ```
1. A config is get value of others
    ``` c
    #define CONFIG_SOMETHING1 "string"
    #define CONFIG_SOMETHING2 0xdead0000
    #define CONFIG_SOMETHING3 123
    ```

