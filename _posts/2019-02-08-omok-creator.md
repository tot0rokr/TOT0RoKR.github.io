---
title: "Omok creator"
last_modified_at: 2019-02-08T11:52:00-09:00
classes: wide
categories:
- Clang
tags:
- clang
excerpt: "variable, loop, conditional만으로 오목 만들기 소스 생성코드"
---

## Intro

어릴 때 만들었던 변수(배열x), 반복문, 조건문 만으로 오목만들기 프로젝트.
반복되는 소스코드 자동생성기.
[이게 완성된 오목코드 소스](https://tot0rokr.github.io/clang/omok-source/)

## 변수선언

``` c
#include <stdio.h>
int main()
{
    int i,j;
    for(i=1;i<=19;i++)
    {
        for(j=1;j<=19;j++)
        {
            if(i<10 && j<10)            // 둘 다 10보다 작을 떄
                printf("Pan0%d0%d, ", i, j);
            else if(i<10 && !(j<10))    //  i만 10보다 작을 때
                printf("Pan0%d%d, ", i, j);
            else if(!(i<10) && j<10)    //  j만 10보다 작을 때
                printf("Pan%d0%d, ", i, j);
            else if(!(i<10) && !(j<10))    // 둘 다 10보다 작지 않을 때
                printf("Pan%d%d, ", i, j);
        }
        printf("\b\b;\n");        // 넘친 , 을 지우고 ; 치고 개행
    }
    return 0;
}
```

## 변수 초기화

``` c
#include <stdio.h>
int main()
{
    int i,j;
    for(i=1;i<=19;i++)
    {
        for(j=1;j<=19;j++)
        {
            if(i<10 && j<10)            // 둘 다 10보다 작을 떄
                printf("Pan0%d0%d=%d0%d, ", i, j, i, j);
            else if(i<10 && !(j<10))    //  i만 10보다 작을 때
                printf("Pan0%d%d=%d%d, ", i, j, i, j);
            else if(!(i<10) && j<10)    //  j만 10보다 작을 때
                printf("Pan%d0%d=%d0%d, ", i, j, i, j);
            else if(!(i<10) && !(j<10))    // 둘 다 10보다 작지 않을 때
                printf("Pan%d%d=%d%d, ", i, j, i, j);
        }
        printf("\b\b;\n");        // 넘친 , 을 지우고 ; 치고 개행
    }
    return 0;
}
```

## 바둑판 출력

``` c
#include <stdio.h>
int main()
{
    int i,j;
    for(i=1;i<=19;i++)
    {
        for(j=1;j<=19;j++)
        {
            /* if 출력 */
            printf("if( ");

            /* 조건문 출력 */
            if(i<10 && j<10)                            
                printf("Pan0%d0%d==%d0%d )", i, j, i, j);
            else if(i<10 && !(j<10))                        
                printf("Pan0%d%d==%d%d )", i, j, i, j);
            else if(!(i<10) && j<10)                        
                printf("Pan%d0%d==%d0%d )", i, j, i, j);
            else if(!(i<10) && !(j<10))    
                printf("Pan%d%d==%d%d )", i, j, i, j);

            /* 바둑판 출력 */
            if(i==1 && j==1)                // 좌표 101
                printf(" printf(\"┌\");\n");                    
            else if(i==1 && j==19)            // 좌표 119
                printf(" printf(\"┐\\n\");\n");
            else if(i==19 && j==1)            // 좌표 1901
                printf(" printf(\"└\");\n");
            else if(i==19 && j==19)            // 좌표 1919
                printf(" printf(\"┘\\n\");\n");
            else if(i==1 && j>=1 && j<=19)    // 좌표 101~119
                printf(" printf(\"┬\");\n");
            else if(i==19 && j>=1 && j<=19)    // 좌표 1901~1919
                printf(" printf(\"┴\");\n");
            else if(i>=1 && i<=19 && j==1)    // 좌표 101~1901
                printf(" printf(\"├\");\n");
            else if(i>=1 && i<=19 && j==19)    // 좌표 119~1919
                printf(" printf(\"┤\\n\");\n");
            else                            // 그 외 전부 다
                printf(" printf(\"┼\");\n");
        


            /* else if 출력 */
            printf("else if( ");

            /* 조건문 출력 */
            if(i<10 && j<10)
                printf("Pan0%d0%d==1 )", i, j, i, j);
            else if(i<10 && !(j<10))
                printf("Pan0%d%d==1 )", i, j, i, j);
            else if(!(i<10) && j<10)
                printf("Pan%d0%d==1 )", i, j, i, j);
            else if(!(i<10) && !(j<10))
                printf("Pan%d%d==1 )", i, j, i, j);

            /* 백돌 출력 */
            if(j==19)                        //백돌이 19번째 열일 경우에 한줄 띄기
                printf(" printf(\"●\\n\");\n");
            else                            //바둑판 대신 백돌을 출력
                printf(" printf(\"●\");\n");
        


            /* else if 출력 */
            printf("else if( ");

            /* 조건문 출력 */
            if(i<10 && j<10)                            
                printf("Pan0%d0%d==2 )", i, j);
            else if(i<10 && !(j<10))                    
                printf("Pan0%d%d==2 )", i, j);
            else if(!(i<10) && j<10)                        
                printf("Pan%d0%d==2 )", i, j);
            else if(!(i<10) && !(j<10))                            
                printf("Pan%d%d==2 )", i, j);

            /* 흑돌 출력 */            
            if(j==19)
                printf(" printf(\"○\\n\");\n");    // 19번째 열 흑돌
            else
                printf(" printf(\"○\");\n");        // 흑돌 출력
        }
    }
    return 0;
}
```

## 바둑판에 돌 추가

``` c 
#include <stdio.h>
int main()
{
    int i,j;
    for(i=1;i<=19;i++)
    {
        for(j=1;j<=19;j++)
        {
            /* 입력한 좌표를 비교 */
            printf("//else if( ");

            /* 조건문 출력 */
            if(i<10 && j<10)    // 좌표와 바둑판의 위치와의 비교
                printf("Pan0%d0%d==xy )\n ", i, j);
            else if(i<10 && !(j<10))                        
                printf("Pan0%d%d==xy )\n ", i, j);
            else if(!(i<10) && j<10)                        
                printf("Pan%d0%d==xy )\n ", i, j);
            else if(!(i<10) && !(j<10))                        
                printf("Pan%d%d==xy )\n ", i, j);

            /* 흑돌 혹은 백돌을 바둑판 변수에 대입 */
            if(i<10 && j<10)    // 좌표와 바둑판이 같을 경우 바둑돌을 파둑판에 대입
                printf("//Pan0%d0%d=turn;\n ", i, j);
            else if(i<10 && !(j<10))                            
                printf("//Pan0%d%d=turn;\n ", i, j);
            else if(!(i<10) && j<10)                        
                printf("//Pan%d0%d=turn;\n ", i, j);
            else if(!(i<10) && !(j<10))                        
                printf("//Pan%d%d=turn;\n ", i, j);
        }                                    
    }
    return 0;
}
```

## 승리체크

``` c
#include <stdio.h>            
int main()                        /*  (y= x 대각선 검사에서 약간의 오류가 있음), 6목 체크안함 */
{
    FILE *out;
    int i,k;
    out=fopen("YES 수정.TXT", "w");

    fprintf(out, "//////////////////////// 가로 검사 ///////////////////////////////////\n");
    for(i=1;i<=19;i++)
    {
        for(k=1;k<=15;k++)
        {
            if(i<10 && k<6)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ win++; } } } } }\n", i, k, i, k+1, i, k+2, i, k+3, i, k+4);

            else if(i<10 && k==6)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d%d==turn) \n{ win++; } } } } }\n", i, k, i, k+1, i, k+2, i, k+3, i, k+4);
            else if(i<10 && k==7)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ win++; } } } } }\n", i, k, i, k+1, i, k+2, i, k+3, i, k+4);
            else if(i<10 && k==8)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ win++; } } } } }\n", i, k, i, k+1, i, k+2, i, k+3, i, k+4);
            else if(i<10 && k==9)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ win++; } } } } }\n", i, k, i, k+1, i, k+2, i, k+3, i, k+4);            
            

            else if(i<10 && !(k<10))    
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ win++; } } } } }\n", i, k, i, k+1, i, k+2, i, k+3, i, k+4);


            else if(!(i<10) && k<6)    
                fprintf(out, "if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i, k+1, i, k+2, i, k+3, i, k+4);
            
            else if(!(i<10) && k==6)    
                fprintf(out, "if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i, k+1, i, k+2, i, k+3, i, k+4);
            else if(!(i<10) && k==7)    
                fprintf(out, "if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i, k+1, i, k+2, i, k+3, i, k+4);
            else if(!(i<10) && k==8)    
                fprintf(out, "if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i, k+1, i, k+2, i, k+3, i, k+4);
            else if(!(i<10) && k==9)    
                fprintf(out, "if(Pan%d0%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i, k+1, i, k+2, i, k+3, i, k+4);


            else if(!(i<10) && !(k<10))
                fprintf(out, "if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i, k+1, i, k+2, i, k+3, i, k+4);
        }
    }

    fprintf(out, "\n/////////////////////// 세로 검사 ////////////////////////////////////\n");
    for(i=1;i<=15;i++)
    {
        for(k=1;k<=19;k++)
        {
            if(i<6 && k<10)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k, i+2, k, i+3, k, i+4, k);
            
            else if(i==6 && k<10)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k, i+2, k, i+3, k, i+4, k);
            else if(i==7 && k<10)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k, i+2, k, i+3, k, i+4, k);
            else if(i==8 && k<10)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k, i+2, k, i+3, k, i+4, k);
            else if(i==9 && k<10)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k, i+2, k, i+3, k, i+4, k);
            

            else if(i<6 && !(k<10))    
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k, i+2, k, i+3, k, i+4, k);
            
            else if(i==6 && !(k<10))        
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k, i+2, k, i+3, k, i+4, k);
            else if(i==7 && !(k<10))        
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k, i+2, k, i+3, k, i+4, k);
            else if(i==8 && !(k<10))        
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k, i+2, k, i+3, k, i+4, k);
            else if(i==9 && !(k<10))        
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k, i+2, k, i+3, k, i+4, k);
            
            
            else if(!(i<10) && k<10)    
                fprintf(out, "if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k, i+2, k, i+3, k, i+4, k);
            
            
            else if(!(i<10) && !(k<10))
                fprintf(out, "if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k, i+2, k, i+3, k, i+4, k);
        }
    }

    fprintf(out, "\n/////////////////////// y = -x 대각선 검사 ////////////////////////////\n");
    for(i=1;i<=15;i++)
    {
        for(k=1;k<=15;k++)
        {
            if(i<6 && k<6)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
            
            else if(i==6 && k==6)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
            else if(i==7 && k==7)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
            else if(i==8 && k==8)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
            else if(i==9 && k==9)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
                        
            
            else if(i<6 && !(k<10))    
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
            
            else if(i==6 && !(k<10))        
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
            else if(i==7 && !(k<10))        
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
            else if(i==8 && !(k<10))        
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
            else if(i==9 && !(k<10))        
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
            
            else if(!(i<10) && k<6)    
                fprintf(out, "if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
            
            else if(!(i<10) && k==6)        
                fprintf(out, "if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
            else if(!(i<10) && k==7)        
                fprintf(out, "if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
            else if(!(i<10) && k==8)        
                fprintf(out, "if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
            else if(!(i<10) && k==9)        
                fprintf(out, "if(Pan%d0%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
                
            
            else if(!(i<10) && !(k<10))
                fprintf(out, "if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k+1, i+2, k+2, i+3, k+3, i+4, k+4);
        }
    }

    fprintf(out, "\n////////////////////// y = x 대각선 검사 //////////////////////////////\n");
    for(i=1;i<=15;i++)
    {
        for(k=5;k<=19;k++)
        {
            if(i<6 && k<10)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            
            else if(i==6 && k<10)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            else if(i==7 && k<10)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            else if(i==8 && k<10)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan0%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            else if(i==9 && k<10)        
                fprintf(out, "if(Pan0%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            
            
            else if(i<6 && !(k<13))    
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            
            else if(i==6 && !(k<13))    
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            else if(i==7 && !(k<13))    
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            else if(i==8 && !(k<13))    
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            else if(i==9 && !(k<13))    
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            
            else if(i==6 && k==13)    
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            else if(i==7 && k==12)    
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            else if(i==8 && k==11)    
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan0%d%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            else if(i==9 && k==10)    
                fprintf(out, "if(Pan0%d%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            
            
            else if(!(i<10) && k<10)    
                fprintf(out, "if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            
            
            else if(!(i<10) && !(k<13))
                fprintf(out, "if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);

            else if(!(i<10) && k==13)
                fprintf(out, "if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            else if(!(i<10) && k==12)
                fprintf(out, "if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            else if(!(i<10) && k==11)
                fprintf(out, "if(Pan%d%d==turn) \n{ if(Pan%d%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
            else if(!(i<10) && k==10)
                fprintf(out, "if(Pan%d%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ if(Pan%d0%d==turn) \n{ win++; } } } } }\n", i, k, i+1, k-1, i+2, k-2, i+3, k-3, i+4, k-4);
        }
    }
    return 0;
}
```
