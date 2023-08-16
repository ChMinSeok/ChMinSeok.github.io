---
layout: single
title: "BOJ 28683번 C++"
date: "date: 2023-08-16 13:40:00 +0900"
categories: [Baekjoon]
tags: [math,Brute force]
background: ''
---
## 풀이
문제에서 한 변이 n이고 나머지 변이 정수인 삼각형의 수를 출력해야한다.  
그렇다면 다음과 같은 삼각형들이 있을 것이다.(n포함)  
>a^2 + b^2 = n

>n + b^2 = c^2

피타고라스 공식을 이용하여 풀 수 있다.  
첫번째 과정은 쉽게 풀 수 있습니다.  
변수 a를잡고 n - (a^2)에 대해서 b^2이 정수인지만 알면 된다.  
(b^2 = n - a^2)  
그렇다면 두번째 과정은 어떻게 수행해야 할까.  
이 문제의 포인트는 두번재 과정이다.  

>n + b^2 = c^2

이식에 대해서 다음과 같은 식을 알아낼 수 있다.  

>n = c^2 - b^2

이걸 곱샘공식을 이용해 나타내면  
>n = (c-b)(c+b)

그렇다면 (c-b)나(c+b)는 n의 약수 일 것이다.  (그렇기에 (c-b)는 정수1)  
그리고 여기서 (c-b)의 값을 알면 c의 값도 알 수 있다.  
>[n / (c-b) = (c+b)] + (c-b) = 2c

그렇다면 여기서 2로 나눈 나머지가 0이라면 c도 정수이기에 한변이 sqrt(n)이고 나머지 변이 정수인 삼각형을 찾을 수 있다.  
  
그렇다면 풀이는 for문을 돌면서 각 포인트에 해당하는 변수를 찾아 대입해보고 조건에 성립하면 삼각형 수를 증가 시킨다.

## 코드
```c++
#include <bits/stdc++.h>
#define X first
#define Y second
#define ll long long

using namespace std;

int dx[4] = {0, 1, -1, 0};
int dy[4] = {1, 0, 0, -1};
int d[2] = {1, -1};

bool isSquere(long long x)
{
    return sqrt(x) == (ll)sqrt(x);
}

int main(void)
{
    ios::sync_with_stdio(0);
    cin.tie(0);
    ll n; cin >> n;
    if(isSquere(n))
        cout << -1;
    else
    {
        ll ans = 0;
        //합동일 수 있는 것을 방지하기 위해 * 2
        for(ll a = 1; a * a * 2 <= n; a++)
        {
            if(isSquere(n - a*a))
                ans++;
        }
        //x를 (c-b)이자 약수라고 생각한다
        //범위가 x*x < n인 이유
        /*
        이 조건을 사용하면 n의 필요한 부분까지만 확인이 가능하다. 
        예를 들어 n이 36이다
        그렇다면 약수들은 (1, 36), (2, 18), (3, 12), (4, 9), (6, 6)
        이제 다시 9,4가 나올 일은 없다 x*x < n을 사용했기에 합동인 중복하는 삼각형을 방지하기 위한 조건이다.
        */
        for(ll x = 1; x * x < n; x++)
        {
            if(n % x == 0 && (x + n/x) % 2 ==0)
                ans++;
        }
        cout << ans;
    }
    return 0;
}
```