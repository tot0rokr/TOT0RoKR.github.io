---
title: "Analysis C Operators"
last_modified_at: 2019-01-01T00:00:00-09:00
categories:
- blog
tags:
- blog
excerpt: "C언어 연산자의 실행속도를 비교분석 해보자(Magic Division을 곁들인)"
---

# 기본 연산들의 operation 속도를 측정-비교해보자

## 사칙연산

### 연산 값이 1인경우

MUL = DIV > ADD > SUB 순으로 속도가 빠르다.

```
add: 35972.570000
div: 23553.610000
mul: 23303.400000
sub: 41171.720000
```

ADD와 SUB는 연산 수는 같지만 연산 자체의 속도 차이가 있는 것을 알 수 있다.

MUL과 DIV의 경우 최적화를 하여 연산 자체를 안한다.
아래 핵심 코드만 보면 연산 자체를 하지 않는 것을 알 수 있다.

```assembly
add:
	addl	$1, -4(%rbp)
	addl	$1, -8(%rbp)
sub:
	subl	$1, -4(%rbp)
	addl	$1, -8(%rbp)
mul:
	addl	$1, -8(%rbp)
div:
	addl	$1, -8(%rbp)
```

### 연산 값이 2인경우

ADD = MUL > SUB > DIV 순으로 속도가 빠르다.

```
add: 35999.910000
div: 69783.050000
mul: 36125.900000
sub: 41972.840000
```

MUL의 경우 shift 연산을 통해 곱셈을 하고 있다.

DIV의 경우 shift 연산을 통해 나눗셈을 하고 있다. -3인 경우 2로 나누면 -1, 3인 경우 2로 나누면 1이
나와야 한다. 그런데 -3을 쉬프트 연산만 하면 -2가 되기 때문에 기존 값에 1을 더해주고(음수이니 빼는
효과) 쉬프트 연산을 하고 있다.


```assembly
add:
	addl	$2, -4(%rbp)
	addl	$1, -8(%rbp)
sub:
	subl	$2, -4(%rbp)
	addl	$1, -8(%rbp)
mul:
	sall	-4(%rbp)
	addl	$1, -8(%rbp)
div:
	movl	-4(%rbp), %eax
	movl	%eax, %edx
	shrl	$31, %edx
	addl	%edx, %eax
	sarl	%eax
	movl	%eax, -4(%rbp)
	addl	$1, -8(%rbp)
```

### 연산 값이 3인경우

ADD > SUB > MUL > DIV 순으로 속도가 빠르다.

이제는 DIV 속도가 현저히 느려지기 시작한다.

```
add: 37361.260000
div: 143092.990000
mul: 46847.060000
sub: 41042.840000
```

MUL을 보면 흥미롭다. 3을 곱하는 것을 2번의 덧셈 연산으로 처리하고 있다. a+a+a = 3a

DIV의 경우에는 굉장히 복잡해졌다. 굉장히 흥미로운데,
찾아보니 3으로 나누는 것을 효율적으로 흉내내기위한 기법(**Magic
Division**)이라고 한다. 매직 넘버 1431655766 (= 0x55555556)를 64비트 정수 곱(imulq)으로 곱한 값의
상위 32비트가 3으로 나눈 결과라고 한다.;;; 위에서 언급한 것처럼 sarl, movl, subl은 음수인 경우 0에 가깝게 만들기
위한(소수점 버리기) 용이다.

```assembly
add:
	addl	$3, -4(%rbp)
	addl	$1, -8(%rbp)
sub:
	subl	$3, -4(%rbp)
	addl	$1, -8(%rbp)
mul:
	movl	-4(%rbp), %edx
	movl	%edx, %eax
	addl	%eax, %eax
	addl	%edx, %eax
	movl	%eax, -4(%rbp)
	addl	$1, -8(%rbp)
div:
	movl	-4(%rbp), %eax
	movslq	%eax, %rdx
	imulq	$1431655766, %rdx, %rdx
	shrq	$32, %rdx
	sarl	$31, %eax
	movl	%eax, %ecx
	movl	%edx, %eax
	subl	%ecx, %eax
	movl	%eax, -4(%rbp)
	addl	$1, -8(%rbp)
```

### 연산 값이 4인경우

ADD = MUL > SUB > DIV 순으로 속도가 빠르다.

MUL과 DIV의 경우에 처리 시간이 다시 짧아졌다.
2의 제곱수를 곱하거나 나누는 것은 쉬프트 연산으로 처리하기 때문이다.

```
add: 36099.800000
div: 101877.350000
mul: 36600.710000
sub: 40781.050000
```

MUL은 ADD나 SUB처럼 하나의 연산으로 처리하고 있다. ADD 연산과 동일한 처리시간을 갖는 것을 알 수
있다.

DIV도 쉬프트 연산으로 처리하는데 흥미로운 점은 leal(eax에 3을 더함)을 덧셈으로 사용하여 쉬프트 시
나누어 떨어지지 않는 값을 버리기 위해 음수인 경우에는 기존 값에 3을 더하고 있다. 이로써 -6을 -1으로
만들 수 있다. 그렇지 않다면 -2가 나오게 된다.


```assembly
add:
	addl	$4, -4(%rbp)
	addl	$1, -8(%rbp)
sub:
	subl	$4, -4(%rbp)
	addl	$1, -8(%rbp)
mul:
	sall	$2, -4(%rbp)
	addl	$1, -8(%rbp)
div:
	movl	-4(%rbp), %eax
	leal	3(%rax), %edx
	testl	%eax, %eax
	cmovs	%edx, %eax
	sarl	$2, %eax
	movl	%eax, -4(%rbp)
	addl	$1, -8(%rbp)
```

### 연산 값이 5인경우

ADD > SUB > MUL > DIV 순으로 속도가 빠르다.

```
add: 36382.720000
div: 163627.380000
mul: 49184.050000
sub: 40298.730000
```

MUL의 경우에는 쉬프트 연산으로 4를 곱하고 1을 더하는 것으로 처리하고 있다. 곱셈 연산이 앵간히
느린가보다. 쉬프트+덧셈으로 처리하는 것이 더 빠르다는 뜻일테니.

DIV의 경우에는 3으로 나누는 것과 마찬가지로 Magic Division을 사용하고 있다. 다만 매직 넘버는 1717986919
(= 0x66666667)이다.

```assembly
add:
	addl	$5, -4(%rbp)
	addl	$1, -8(%rbp)
sub:
	subl	$5, -4(%rbp)
	addl	$1, -8(%rbp)
mul:
	movl	-4(%rbp), %edx
	movl	%edx, %eax
	sall	$2, %eax
	addl	%edx, %eax
	movl	%eax, -4(%rbp)
	addl	$1, -8(%rbp)
div:
	movl	-4(%rbp), %eax
	movslq	%eax, %rdx
	imulq	$1717986919, %rdx, %rdx
	shrq	$32, %rdx
	sarl	%edx
	sarl	$31, %eax
	movl	%eax, %ecx
	movl	%edx, %eax
	subl	%ecx, %eax
	movl	%eax, -4(%rbp)
	addl	$1, -8(%rbp)
```


## 실행 코드

```c
#include <time.h>
#include <stdio.h>

#define MEASURE(__t, __n, __func) printf("%s: %lf\n", (#__func), measure(__t, __n, (__func)))

#define NUM 5

int add(int n) {
	int i, j;
	int tmp = 0;

	for (i = 0; i < n; i++) {
		tmp += NUM;
	}
}

int sub(int n) {
	int i, j;
	int tmp = 0;

	for (i = 0; i < n; i++) {
		tmp -= NUM;
	}
}

int mul(int n) {
	int i, j;
	int tmp = 0;

	for (i = 0; i < n; i++) {
		tmp *= NUM;
	}
}

int div(int n) {
	int i, j;
	int tmp = 0;

	for (i = 0; i < n; i++) {
		tmp /= NUM;
	}
}

double measure(int t, int n, int (*cb)(int)) {
	int i;
	double sum;
	clock_t start, end;

	for (i = 0; i < t; i++) {
		start = clock();
		cb(n);
		end = clock();
		sum += (double)(end - start);
	}
	return sum / t;
}

int main() {
	int t = 100;
	int n = 100000000;

	MEASURE(t, n, add);
	MEASURE(t, n, div);
	MEASURE(t, n, mul);
	MEASURE(t, n, sub);


	return 0;
}
```
