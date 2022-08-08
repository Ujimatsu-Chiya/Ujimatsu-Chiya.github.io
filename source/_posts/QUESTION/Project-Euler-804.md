---
title: Project Euler 804
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-19 00:28:38
---

<escape><!-- more --></escape>

# Project Euler 804

## 题目

### Balanced Numbers

Let $g(n)$ denote the number of ways a positive integer $n$ can be represented in the form:

$$x^2+xy+41y^2$$

where $x$ and $y$ are integers. For example, $g(53)=4$ due to $(x,y) \in \{(-4,1),(-3,-1),(3,1),(4,-1)\}$.

Define $\displaystyle T(N)=\sum_{n=1}^{N}g(n)$. You are given $T(10^3)=474$ and $T(10^6)=492128$.

Find $T(10^{16})$.

## 解决方案

令$N=10^{16},F(x,y)=x^2+xy+41y^2$。不难证明，$F(x,y)>0$恒成立，除了$(x,y)=(0,0)$。

因此，$T(N)$的值就相当于有多少个非原点$(x,y)$，满足$F(x,y)\le N$。

固定$y$，那么可以将$F(x,y)$写成顶点式：

$$F(x,y)=(x+\dfrac{y}{2})^2+\dfrac{163y^2}{4}$$

枚举$y$，然后解不等式$F(x,y)\le N$即可，直到方程无解。

为了排除$(0,0)$的情况，单独考虑$y=0$时的情况，这时有$2\lfloor\sqrt{N}\rfloor$个解。

否则，区间$[\dfrac{-y-\sqrt{4N-163y^2}}{2},\dfrac{-y+\sqrt{4N-163y^2}}{2}]$种的所有整数解都是答案，直接统计即可。

## 代码

```C++
#include <bits/stdc++.h>
# include "tools.h"
typedef long long ll;
using namespace std;
const ll N=1e16;
int main(){
    ll ans=int_sqrt(N)*2;
    for(ll i=1,d2;(d2=N*4-i*i*163)>=0;i++){
        ll r=-i+int_sqrt(d2);
        if(r<0&&r&1) --r;
        r>>=1;
        ll l=-i-r;
        ans+=(r-l+1)*2;
    }
    printf("%lld\n",ans);
}

```
