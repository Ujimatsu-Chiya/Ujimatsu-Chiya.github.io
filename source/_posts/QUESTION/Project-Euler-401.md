---
title: Project Euler 401
category:
  - Project Euler
tags:
  - 数论分块
mathjax: true
date: 2022-06-05 09:28:58
---

<escape><!-- more --></escape>

# Project Euler 401

## 题目

### Sum of squares of divisors

The divisors of $6$ are $1,2,3$ and $6$.

The sum of the squares of these numbers is $1+4+9+36=50$.

Let $\text{sigma2}(n)$ represent the sum of the squares of the divisors of n. Thus $\text{sigma2}(6)=50$.

Let $\text{SIGMA2}$ represent the summatory function of $\text{sigma2}$, that is $\text{SIGMA2}(n)=\sum\text{ sigma2}(i)$ for $i=1$ to $n$.

The first $6$ values of SIGMA2 are: $1,6,16,37,63$ and $113$.

Find $\text{SIGMA2}(10^{15}) \text{ modulo } 10^9$.

## 数论分块

这种方法一般用于计算关于某个函数$f$（$f$的前缀和$s(n)$可以很轻松地算出来）的下面的表达式：

$$g(n)=\sum_{d=1}^nf(d)\cdot \left\lfloor\dfrac{n}{d}\right\rfloor$$

对于$d$任意不同的取值，$\left\lfloor\dfrac{n}{d}\right\rfloor$只有$O(\sqrt{n})$个值。

一个块如果下标从$i$开始，那么到$\left\lfloor\dfrac{n}{\left\lfloor\frac{n}{i}\right\rfloor}\right\rfloor$才结束，而这块内部的所有$\left\lfloor\dfrac{n}{d}\right\rfloor$都是相同的。下一个块的起点为$\left\lfloor\dfrac{n}{\left\lfloor\frac{n}{i}\right\rfloor}\right\rfloor+1$开始，这些块是首尾相接的。

因此，从下标$i=1$开始，枚举计算每一块的$f$函数之和，并求和，用表达式来表示就是：

$$g(n)=\sum_{k}\left\lfloor\dfrac{n}{k}\right\rfloor\cdot\left(s\left(\left\lfloor\dfrac{n}{\left\lfloor\frac{n}{k}\right\rfloor}\right\rfloor\right)-s(k-1)\right)$$

其中$k$是每一块的起点。

## 解决方案

不难想到每个因子$d$在$1\sim n$中出现的次数总共为$\left\lfloor\dfrac{n}{d}\right\rfloor$次。

因此$\text{SIGMA2}(n)=\sum_{i=1}^n\left\lfloor\dfrac{n}{d}\right\rfloor\cdot d^2$。

代入数论分块中，$f(n)=n^2$，那么$s(n)=\dfrac{n(n+1)(2n+1)}{6}$即可。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N=1e15;
ll mod=1e9;
ll inv3=666666667;
ll f(ll n){
    n%=mod;
    return n*(n+1)/2%mod*(n+n+1)%mod*inv3%mod;
}
int main(){
    ll ans=0,x;
    for(x=1;x*x<=N;x++){
        ans=(ans+N/x%mod*x%mod*x)%mod;
    }
    for(ll y;x<=N;x=y+1){
        y=N/(N/x);
        ll c=(N/x)%mod;
        ans=(ans+(f(y)-f(x-1)+mod)*c)%mod;
    }
    printf("%lld\n",ans);
}

```
