---
title: Project Euler 688
tags:
  - Project Euler
  - 贪心
mathjax: true
date: 2022-07-17 23:11:25
---

<escape><!-- more --></escape>

# Project Euler 688

## 题目

### Piles of Plates

We stack $n$ plates into $k$ non-empty piles where each pile is a different size. Define $f(n,k)$ to be the maximum number of plates possible in the smallest pile. For example when $n = 10$ and $k = 3$ the piles $2,3,5$ is the best that can be done and so $f(10,3) = 2$. It is impossible to divide $10$ into $5$ non-empty differently-sized piles and hence $f(10,5) = 0$.

Define $F(n)$ to be the sum of $f(n,k)$ for all possible pile sizes $k\ge 1$. For example $F(100) = 275$.

Further define $S(N) = \displaystyle\sum_{n=1}^N F(n)$. You are given $S(100) = 12656$.

Find $S(10^{16})$ giving your answer modulo $1\,000\,000\,007$.

## 解决方案

令$N=10^{16}.$

如果$n$个盘子放成$k$堆，那么一种贪心的方法则是先摆成$1,2,3,\dots,k-1,k$这$k$堆，接下来将剩下的$n-\dfrac{k(k+1)}{2}$碟子再均分到这$k$堆，如果剩下的碟子依然不能均分，那么全部都分给最大的那堆。因此不难写出函数$f$为：

$$
f(n,k)=
\left \{\begin{aligned}
  &0  & & \mathrm{if\quad} n<\dfrac{k(k+1)}{2} \\
  &1+\lfloor\dfrac{n}{k}-\dfrac{k+1}{2}\rfloor & & \mathrm{else}
\end{aligned}\right.
$$

不过，这个式子其实对解题并没有太大的帮助。

将$S$的定义式子进行改写：

$$S(N)=\sum_{n=1}^N\sum_{k\ge 1}f(n,k)=\sum_{1\le \frac{k(k+1)}{2}\le N}\sum_{n=\frac{k(k+1)}{2}}^{N}f(n,k)$$

本质上，是将$n,k$的枚举顺序改变了。

式子$\sum_{n=\frac{k(k+1)}{2}}^{N}f(n,k)$的值可以以$O(1)$的时间复杂度进行计算。因为按照此时$n$枚举顺序，$f(n,k)$将会是连续$k$个$1$，$k$个$2$，……考虑分块然后使用等差数列求和进行计算。

令$x=N-\dfrac{k(k+1)}{2}+1$，$q=\lfloor\dfrac{x}{k}\rfloor,r=x\%k$，那么分块后计算得$\sum_{n=\frac{k(k+1)}{2}}^{N}f(n,k)=k\cdot\dfrac{q\cdot(q+1)}{2}+(q+1)\cdot r$。

最终枚举$k$并将这些值相加即可。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const ll Q=1e16;
ll mod=1e9+7;
ll inv2=(mod+1)>>1;
int main(){
    ll ans=0;
    for(ll k=1;;k++){
        ll w=k*(k+1)/2;
        if(w>Q) break;
        ll t=Q-w+1;
        ll q=t/k%mod,r=t%k;
        ans=(ans+k*q%mod*(q+1)%mod*inv2%mod+(q+1)*r%mod)%mod;
    }
    printf("%lld\n",ans);
}

```
