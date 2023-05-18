---
layout: single
title: "C/C++ 포인터 기본2"
date: "date: 2023-05-18 01:30:00 +0900"
categories: [C++]
tags: [C++ 기초, pointer]
background: ''
---
여러 가지 예를 보겠습니다.  
### 디레퍼런싱
```c++
int a;
int *p;
a = 10;
p = &a; //a의 주소
cout << a; //10이 나옴
*p = 12; // dereferencing
cout << a; //12가 나옴
```
```c++
int a;
int *p;
a = 10;
p = &a; //a의 주소
printf("p가 가리키는 주소는 %d\n",p);
printf("p의 값은 %d\n",*p);
int b = 20;
*p = b; // 주소가 b를 가리키게 바뀔까?
printf("p가 가리키는 주소는 %d\n",p);
printf("p의 값은 %d\n",*p);
```
p의 주소는 안바뀌고 p의 값만 바뀌였습니다.  
### 포인터 산수
포인터 산수는 가능합니다. 주소에 산수가 가능하다는거죠.   
어떻게 될까요. 예를 봅시다.
```c++
 int a;
    int* p = &a;
    printf("p주소 = %d\n", p); //p가 2002라 칩시다.
    printf("인트 사이즈%d\n", sizeof(int)); //size = 4byte
    printf("p주소 + 1 = %d\n", p + 1); //2006;
```
int의 사이즈는 4죠 int 포인터에 1을 더하면 4가 증가 char포인터에 1을 더하면 1이 증가합니다.
