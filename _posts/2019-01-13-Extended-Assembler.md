---
title: "Extended Assembler"
last_modified_at: 2019-01-13T09:43:00-09:00
categories:
- Kernel
- Assembler
tags:
- kernel
- gcc
- assembler
excerpt: "GNU gcc의 확장된 어셈블리어. C언어의 표현식(변수나 goto label)을 사용하기 위함."
---

# Extended Asm - Assembler Instructions with C Expression Operands

>https://gcc.gnu.org/onlinedocs/gcc/Extended-Asm.html

이 글은 위의 gnu gcc 문서를 읽기 쉽게 번역했음을 알립니다. 세부 사항은 직접 확인해주세요.

## 기능

assmbler instructions의 input과 output을 C언어의 변수에 저장할 수 있고, jump label을 c언어의 goto label로 이용 할 수 있는 명령입니다.

**점프 없을 시:**
```
asm asm-qualifiers ( AssemblerTemplate 
                 : OutputOperands 
                 [ : InputOperands
                 [ : Clobbers ] ])
```
**점프 있을 시:**
```
asm asm-qualifiers ( AssemblerTemplate 
                      : 
                      : InputOperands
                      : Clobbers
                      : GotoLabels)
```


### Qualifiers

`asm asm-qualifiers` 의 qualifiers에 들어가는 사항입니다.

- volatile : 최적화 중지.
- inline : 인라인으로 사용하기 위한 asm을 사용.
- goto : GotoLabels 로 jump 하는 코드를 사용하기 위한 수식.

### Parameters

- AssemblerTemplate : 어셈블리 코드가 들어가는 부분. Template는 아래를 참조하세요.
> https://gcc.gnu.org/onlinedocs/gcc/Extended-Asm.html#AssemblerTemplate
- OutputOperands : 출력 변수가 들어감. 없으면 비우는 것이 가능.
- InputOperands : 입력 변수가 들어감. 없으면 비우는 것이 가능.
- Clobbers : Input과 Output에서 사용되지 않는 추가적인 레지스터가 필요할 때 들어감. counting을 위한 목적 같은. 없으면 비우는 것이 가능.
- GotoLabels : asm 에서 branch 명령의 레이블로 C언어 label을 사용하기 위함. 이 파라미터로 지정한 label이외에 다른 asm의 label로 jump하지 못할 수 있음. (Optimizer가 다른 jump label을 모를 수 있음)

모든 파라미터는 콤마(,)로 구분되며, 총 operands는 30개로 제한.

### Remarks

확장 asm은 C 프로그램의 함수 안에 존재해야함. 함수 밖에서는 기본 asm 명령어밖에 사용 불가능.


### 예시1 (jump가 없을 때)

```
int src = 1;
int dst;   

asm ("mov %1, %0\n\t"
    "add $1, %0"
    : "=r" (dst) 
    : "r" (src));

printf("%d\n", dst);
```

- `\n\t` : asm 의 두 instruction을 사용하기 위한 구분.
- `mov` : 값을 이동.
- `"=r" (dst)` : register 에 dst 변수를 넣어서 asm의 %0으로 사용하겠다.( 맨 처음 나온 operand부터
0, 1, 2... 순서대로 번호가 붙음.)
- `"r" (src)` : register에 src 변수를 넣어서 asm의 %1으로 사용하겠다는 의미. 
- `mov %1, %0` :  dst에 src의 값을 넣음.
- `add $1, %0` : dst에 1의 값을 더함.

> 라고 문서에 나옴. 문서가 i386을 기준으로 작성 된 것이라서 arm64와 문법이 다를 수도 있고 아닐 수도 있음. (gnu gcc에서 동작하는 문법이라서 문법이 같을 수도 있음. 사실 잘 모르겠음. 원래 intel asm dst가 앞이고 src가 뒤 아닌가?)


### 예시2 (jump가 있을 때)

jump가 있을 때는 **Output이 존재하면 안됨.** 위에도 일부러 비워놓은 것임.

**i386 예제:**
```
int frob(int x)
{
  int y;
  asm goto ("frob %%r5, %1; jc %l[error]; mov (%2), %%r5"
            : /* No outputs. */
            : "r"(x), "r"(&y)
            : "r5", "memory" 
            : error);
  return y;
error:
  return -1;
}
```

- `%%` : %를 출력하기 위한 C언어에서 그것.
- `frob %%r5, %1` : frob이 무슨 명령인지는 모르겠음. 찾아도 안나옴. 아무튼 비교문인 것 같음.
왜 %0부터 시작하지 않는지 도무지 이해할 수 없음. 뭐 오탄가보다 함. 알려주셈ㅠㅠ.
%r5 즉, 실제 r5 레지스터에 저장된 데이터 값과 x를 비교하는 듯.
- `error` : 4번째 parameter. Jump Label을 지정하는 위치. C언어에서의 error 라벨이다.
- `%l` : jump할 곳의 라벨의 자리를 의미한다.
- `[error]` : 직접 이름을 지정하기 위한 방법으로 보임. 2나 3같은 숫자가 들어가도 됨.
- `jc %l[error]` : carry flag가 set되면 error 라벨로 점프.
- `mov (%2), %%r5` : &y. 즉, y의 위치를 참조(메모리 접근)하여 그 공간에 r5 레지스터의
값을 저장.
> 이건 100% y의 메모리 주소를 참조해서(*y)에 r5 레지스터의 값을 넣으라는 의미임.
> 너무나도 당연함. y는 아직 값이 없고, 이 명령 이후에 y를 리턴함. 근데 여기선 왜 src가
>  뒤고 dst가 앞이지?????
- `"r5"` : 추가적으로 r5 레지스터를 사용하는 부분이 있다고 명시. (안해주면 안됨;)
- `"memory"` : 메모리를 접근하는 부분이 있다고 명시. (해줘야됨;)


## 결론
~진짜 짜증난다. 문서가 잘못된걸까? 제발 나에게 진실을 알려줘~~
