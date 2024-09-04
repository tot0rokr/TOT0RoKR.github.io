---
title: "Weird C-lang coding technique with Linux"
last_modified_at: 2024-09-04T00:00:00-09:00
categories:
- C
tags:
- linux
- zephyr
- bluez
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
