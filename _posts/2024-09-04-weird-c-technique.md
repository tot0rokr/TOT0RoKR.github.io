---
title: "Weird C-lang coding technique with Linux"
last_modified_at: 2024-09-05T00:00:00-09:00
categories:
- C
tags:
- linux
- zephyr
- bluez
- clang
excerpt: "종나 이상한 C언어 테크닉(하지만 리눅스를 곁들인)"
---

Linux Kernel 분석할 때 상당히 많이 봤는데 정리해둘걸 아쉽지만 지금이라도 신기하고 이상한 테크닉을
소개하려고 한다.

## Built-in dynamic memory allocation

자료구조 내에 built-in 된 buf 배열을 동적으로 길이를 늘릴 수 있을까? **오버플로우**를 사용하면 된다.

```c
struct pdu {
    uint8_t len_buf;
    uint8_t buf[0];     /* Zero size */
};

struct pdu *new_pdu(uint8_t len)
{
    int size = sizeof(struct pdu) + len;
    return (struct pdu *)malloc(size);
}
```

`struct pdu`를 할당 시에 원하는 만큼 더 크게 할당 받고 사용 시에는 원래 배열처럼 사용하면 된다.
C언어는 인덱스 체크 따위를 하지 않는 특징을 이용한 개쩌는 테크닉.

BlueZ 프로젝트에서 발견할 수 있다.

### 예제

https://github.com/tot0rokr/practice/blob/main/c/c-overflow-allocation/main.c

## Integer to Bool

integer 타입을 bool 타입으로 바꾸는 테크닉. 에러코드를 리턴하거나 length가 0보다 큰 경우 등을
확인하는 데에 사용한다.

이건 종종 보일법한 테크닉이다. 처음 봤을 때는 이건 뭔 헛짓거리지 라고 생각했지만 깨달은 이후 종종
보인다.

```c
#include <stdbool.h>
#define EXCEPTION 1

bool some_procedure(int len)
{
    int err = 0;
    if (!!len) {
        err = -EXCEPTION;
        goto out;
    }

out:
    return !!err;
}
```

Linux Foundation에서 개발한 프로젝트에서는 웬만해서 발견할 수 있다.

## Like yeild

마치 Iterator(혹은 Generator, Enumerator) 처럼 yield를 구현하는 방법이다. 타이머를 통한 스케줄링
등을 통해 반복 수행함으로써 프로시저를 진행한다.

```c
void send_seg_tx(struct tx *tx)
{
    while (tx->seg_o <= tx->seg_n) {
        struct pdu *pdu;
        int err;

        if (tx->ack[tx->seg_o]) {
            tx->seg_o++;
            continue;
        }

        pdu = build_buf(tx, tx->seg_o);
        err = send_pdu(pdu);

        if (!!err) {
            return false;
        }

        goto next;
    }
    return true;
next:
    reschedule(tx, tx->interval);
}
```

이런 식으로 이미 진행한 부분은 continue로 건너뛰고, 정상동작하면 reschedule을 해서 결국 반복문을
전부 수행할 수 있는 구조를 가진다.

Zephyr 프로젝트에서 발견할 수 있다.

## Linked List

Linux Kernel의 linked-list는 매우 단순하고, 모든 struct 자료구조에서 재사용할 수 있는 범용적 형태를
취하고 있다. 하지만 단점은 표준 방식이 아니기에 모든 컴파일러에서 해석되지 않을 가능성이 존재한다.
애초에 `({expresstion})` 표현식 자체가 Microsoft VS 컴파일러에서 해석이 안된다_(201x년도에 확인함)_.
GCC로 컴파일 해야 컴파일 된다.

### list_head

```c
/* in include/linux/types.h */
struct list_head {
    struct list_head *next, *prev;
};
```

### example struct

```c
struct my_struct {
    char* foo;
    char* bar;
    /* ... other fields ... */
    struct list_head list;
};
```

### offsetof

```c
/* in include/linux/stddef.h */
#undef offsetof
#ifdef __compiler_offsetof
#define offsetof(TYPE,MEMBER) __compiler_offsetof(TYPE,MEMBER)
#else
#define offsetof(TYPE, MEMBER) ((size_t) &((TYPE *)0)->MEMBER)
#endif
```

### container_of

```c
/* in include/kernel.h */
#define container_of(ptr, type, member) ({                          \
            const typeof( ((type *)0)->member ) *__mptr = (ptr);    \
            (type *)( (char *)__mptr - offsetof(type,member) );})
```

`list_head`는 매우 간단하다. 간단하기에 재사용이 쉽다. 사용하고자 하는 자료구조에 멤버변수로
추가하기만 하면 사용할 수 있다.

`offsetof`를 보면 주소값 0에서 멤버변수 접근으로 해당 object의 `list_head` 필드의 offset을 알아낸
뒤, 실제 `list_head` 필드의 주소에 offset을 빼서 object의 주소를 알아낸다. 그 다음 해당 자료구조로
타입캐스팅을 하면 끝이다.

Linked-list 뿐만 아니라 tree구조 등 자료구조는 모두 동일한 방법으로 사용 가능하다.

## Address combined data

Linux Kernel에는 현재 대부분 Maple Tree로 대체된 Red-Black Tree(RBTree)가 있다. kernel에서 RBTree는
메모리를 절약하기 위해 해괴한 방법을 사용하는데, 이는 address에 data를 결합하는 방법이다.

```c
struct rb_node {
    unsigned long  __rb_parent_color; /* rb parent and color */
    struct rb_node *rb_right;
    struct rb_node *rb_left;
} __attribute__((aligned(sizeof(long))));
```

`aligned(sizeof(long))` attribute를 사용해서 해당 자료구조를 할당 시에 long 타입 길이 단위로
정렬한다. 그려면 32-bit(혹은 64-bit) 시스템에서는 4바이트(혹은 8바이트) 단위로 메모리가 정렬되어
주소값의 하위 2비트(혹은 3비트)가 0임이 보장된다. 이를 이용하여 해당 2비트(혹은 3비트)에 데이터를
주소값과 함께 long타입에 저장하는 테크닉이 존재한다.

단점은 저대로 주소에 접근하면 당연히 잘못된 주소에 접근하게 되므로 encoding/decoding이 필요하며,
매번 타입캐스팅도 해주어야 한다. 하지만 RBTree에서 parent의 주소는 오직 rotation 되는 동작에서만
필요하기 때문에 탐색과정의 시간을 줄이고자 하는 RBTree의 특성상 크게 성능에 지장을 주지 않는다.
오히려 메모리를 아끼면서 얻게되는 캐시 히트율에 더 큰 성능 향상을 기대할 수 있다.
