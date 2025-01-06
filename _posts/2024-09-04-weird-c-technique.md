---
title: "Weird C-lang coding technique with Linux"
last_modified_at: 2025-01-06T00:00:00-09:00
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
실 사용 사례와 함께 소개하려고 한다. 만약 추가적으로 생각나거나 알게 되는 것이 있으면 더 추가할
예정이다.

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
C언어는 인덱스나 길이 체크 따위를 하지 않는 특징을 이용한 개쩌는 테크닉.

BlueZ 프로젝트나 Linux Kernel 프로젝트에서 Packet Data 자료구조에서 발견할 수 있다.

#### 예제

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

마치 Iterator(혹은 Generator, Enumerator) 처럼 yield를 구현하는 방법이다. 엄현히 따지자면 다르지만
Iterator 반복마다 Block을 하는 프로시저라면 유사하다고 볼 수 있다. 타이머를 통한 스케줄링
등을 통해 반복 수행함으로써 한 스텝씩 프로시저를 진행한다.

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

#### list_head

```c
/* in include/linux/types.h */
struct list_head {
    struct list_head *next, *prev;
};
```

#### example struct

```c
struct my_struct {
    int foo;
    char* bar;
    /* ... other fields ... */
    struct list_head list;
};
```

#### offsetof

```c
/* in include/linux/stddef.h */
#undef offsetof
#ifdef __compiler_offsetof
#define offsetof(TYPE,MEMBER) __compiler_offsetof(TYPE,MEMBER)
#else
#define offsetof(TYPE, MEMBER) ((size_t) &((TYPE *)0)->MEMBER)
#endif
```

#### container_of

```c
/* in include/kernel.h */
#define container_of(ptr, type, member) ({                          \
            const typeof( ((type *)0)->member ) *__mptr = (ptr);    \
            (type *)( (char *)__mptr - offsetof(type,member) );})
```

`list_head`는 매우 간단하다. 간단하기에 재사용이 쉽다. 사용하고자 하는 자료구조에 멤버변수로
추가하기만 하면 사용할 수 있다.

`offsetof`를 인스턴스 내 `list_head`의 offset을 알아내기 위해 사용한다. `container_of`는 이 offset을
이용하여 인스턴스의 포인터를 알아내는 매크로이다.

`list_head`를 통해 `my_struct`의 포인터를 얻기 위해 아래와 같이 사용할 수 있다.

```c
struct my_struct *my_struct_from_entry(struct list_head *head)
{
    return container_of(head, struct my_struct, list);
}
```

Linked-list 뿐만 아니라 Tree 구조와 같은 Link를 사용하는 자료구조 모두 동일한 방법으로 사용 가능하다.

## For-each statement

C언어에는 for-each 구문이 없다. 그래서 다양한 프로젝트에서 다양한 방법으로 for-each 구문을 구현하고
있다. 여기서 몇가지 방법을 소개한다.

### array_for_each

배열을 순회하기 위한 for-each 구문을 사용할 수 있다. 이는 아래와 같이 `sizeof`를 이용하여 구현된다.
여기서 `pos`는 각 요소, `array`는 배열이다.

```c
#define array_for_each(pos, array)                                     \
    for (pos = (array);                                                 \
         pos < (array) + sizeof(array) / sizeof(array[0]);              \
         pos++)


void func()
{
    int array[] = {1, 2, 3, 4, 5};
    int *pos;

    array_for_each(pos, array) {
        printf("%d\n", *pos);
    }
}
```

#### list_for_each_entry

Linked-list entry를 순회하기 위한 for-each 구문을 사용할 수 있다. 이는 아래와 같이 `container_of`를
이용하여 구현된다. 여기서 `pos`는 요소, `head`는 리스트의 헤드노드, `member`는 요소의 리스트
멤버이다.

```c
#define list_for_each_entry(pos, head, member)                          \
    for (pos = container_of((head)->next, typeof(*pos), member);        \
         &pos->member != (head);                                        \
         pos = container_of(pos->member.next, typeof(*pos), member))

void func()
{
    struct my_struct *pos;
    struct list_head *head;

    /* 리스트 초기화 및 삽입과정 생략 */

    list_for_each_entry(pos, head, list) {
        printf("%d\n", pos->foo);
    }
}
```



## Compress data structure size using aligned address

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

## Inheritance

Linux Kernel에서 네트워크 소켓 자료구조를 보면 일종의 상속을 사용한다. 하위 계층에 사용하는 소켓
자료구조를 상위 계층 소켓이 첫 번째 필드로 가져가며, define 매크로를 통해 다이렉트로 접근하는 것처럼
하여 상위계층 소켓을 감춘다. 이렇게 하여 네트워크 전체 계층에서 사용하는 소켓에 대한 메모리를 한번에
할당하여 이득을 취한다.

```c
/* In include/net/inet_sock.h */
struct inet_sock {
	/* sk and pinet6 has to be the first two members of inet_sock */
	struct sock		sk;
#if IS_ENABLED(CONFIG_IPV6)
	struct ipv6_pinfo	*pinet6;
#endif
	/* Socket demultiplex comparisons on incoming packets. */
#define inet_daddr		sk.__sk_common.skc_daddr
#define inet_rcv_saddr		sk.__sk_common.skc_rcv_saddr
#define inet_dport		sk.__sk_common.skc_dport
#define inet_num		sk.__sk_common.skc_num

	__be32			inet_saddr;
	__s16			uc_ttl;
	__u16			cmsg_flags;
	__be16			inet_sport;
	__u16			inet_id;

    /*
     * Leave out...
     */

};
```

```c
/* In include/net/sock.h */
struct sock {
	/*
	 * Now struct inet_timewait_sock also uses sock_common, so please just
	 * don't add nothing before this first member (__sk_common) --acme
	 */
	struct sock_common	__sk_common;
#define sk_node			__sk_common.skc_node
#define sk_nulls_node		__sk_common.skc_nulls_node
#define sk_refcnt		__sk_common.skc_refcnt
#define sk_tx_queue_mapping	__sk_common.skc_tx_queue_mapping
#ifdef CONFIG_XPS
#define sk_rx_queue_mapping	__sk_common.skc_rx_queue_mapping
#endif

#define sk_dontcopy_begin	__sk_common.skc_dontcopy_begin
#define sk_dontcopy_end		__sk_common.skc_dontcopy_end
#define sk_hash			__sk_common.skc_hash
#define sk_portpair		__sk_common.skc_portpair
#define sk_num			__sk_common.skc_num
#define sk_dport		__sk_common.skc_dport
#define sk_addrpair		__sk_common.skc_addrpair
#define sk_daddr		__sk_common.skc_daddr
#define sk_rcv_saddr		__sk_common.skc_rcv_saddr
#define sk_family		__sk_common.skc_family
#define sk_state		__sk_common.skc_state
#define sk_reuse		__sk_common.skc_reuse
#define sk_reuseport		__sk_common.skc_reuseport
#define sk_ipv6only		__sk_common.skc_ipv6only
#define sk_net_refcnt		__sk_common.skc_net_refcnt
#define sk_bound_dev_if		__sk_common.skc_bound_dev_if
#define sk_bind_node		__sk_common.skc_bind_node
#define sk_prot			__sk_common.skc_prot
#define sk_net			__sk_common.skc_net
#define sk_v6_daddr		__sk_common.skc_v6_daddr
#define sk_v6_rcv_saddr	__sk_common.skc_v6_rcv_saddr
#define sk_cookie		__sk_common.skc_cookie
#define sk_incoming_cpu		__sk_common.skc_incoming_cpu
#define sk_flags		__sk_common.skc_flags
#define sk_rxhash		__sk_common.skc_rxhash

	socket_lock_t		sk_lock;
	atomic_t		sk_drops;
	int			sk_rcvlowat;
	struct sk_buff_head	sk_error_queue;
	struct sk_buff_head	sk_receive_queue;

    /*
     * Leave out...
     */
};
```

```c
/* In include/net/sock.h */
struct sock_common {
	/* skc_daddr and skc_rcv_saddr must be grouped on a 8 bytes aligned
	 * address on 64bit arches : cf INET_MATCH()
	 */
	union {
		__addrpair	skc_addrpair;
		struct {
			__be32	skc_daddr;
			__be32	skc_rcv_saddr;
		};
	};
	union  {
		unsigned int	skc_hash;
		__u16		skc_u16hashes[2];
	};
	/* skc_dport && skc_num must be grouped as well */
	union {
		__portpair	skc_portpair;
		struct {
			__be16	skc_dport;
			__u16	skc_num;
		};
	};

    /*
     * Leave out...
     */

	refcount_t		skc_refcnt;
	/* private: */
	int                     skc_dontcopy_end[0];
	union {
		u32		skc_rxhash;
		u32		skc_window_clamp;
		u32		skc_tw_snd_nxt; /* struct tcp_timewait_sock */
	};
	/* public: */
};
```

이렇게 하면 `struct inet_sock`의 인스턴스인 `inet`에 대하여 `inet.daddr`을 통해서 `struct
sock_common`에 있는 `sock_daddr` 필드를 접근할 수 있게 한다.
여기서 장점은 ip 프로토콜에서 사용하는 소켓인 `struct inet_sock` 뿐만 아니다 다른 프로토콜에서도
`struct sock_common`을 상속하여 동일한 API를 사용할 수 있다는 것이 장점이다.
