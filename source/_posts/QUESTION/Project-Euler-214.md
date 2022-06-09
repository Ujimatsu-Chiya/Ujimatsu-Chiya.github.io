---
title: Project Euler 214
tags:
  - Project Euler
  - 动态规划
mathjax: true
date: 2022-05-30 20:28:27
---

<escape><!-- more --></escape>

# Project Euler 214

## 题目

### Totient Chains

Let $\varphi$ be Euler’s totient function, i.e. for a natural number n, $varphi(n)$ is the number of $k, 1 \le k \le n,$ for which $\gcd(k,n) = 1$.

By iterating $\varphi$, each positive integer generates a decreasing chain of numbers ending in $1$. E.g. if we start with $5$ the sequence $5,4,2,1$ is generated.

Here is a listing of all chains with length $4$:

$\begin{aligned}
& 5,4,2,1\\
& 7,6,2,1\\
& 8,4,2,1\\
& 9,6,2,1\\
& 10,4,2,1\\
& 12,4,2,1\\
& 14,6,2,1\\
& 18,6,2,1
\end{aligned}$

Only two of these chains start with a prime, their sum is $12$.
What is the sum of all primes less than $40000000$ which generate a chain of length $25$?

## 解决方案

令$N=40000000,M=25$。

本题使用的$N$的范围比较大，不难想到使用线性筛来计算积性函数$\varphi$的值。

设$f(i)(i\ge 1)$为以$i$为起点的链长度，根据题意，不难想到使用动态规划的方法来计算$f(i)$：

$$
f(i)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=1 \\
  &f(\varphi(i))+1 & & \mathrm{else}
\end{aligned}\right.
$$

遍历所有$N$以内的质数，判断其$f$的函数值是否为$M$。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=40000000,M=25;
int f[N+4],phi[N+4],pr[N+4],v[N+4];
int m=0;
int main(){
    phi[1]=f[1]=1;
    for(int i=2;i<N;i++){
        if(v[i]==0){
            v[i]=i;phi[i]=i-1;
            pr[++m]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
            if(pr[j]==v[i]) phi[i*pr[j]]=phi[i]*pr[j];
            else phi[i*pr[j]]=phi[i]*(pr[j]-1);
        }
        f[i]=f[phi[i]]+1;
    }
    ll ans=0;
    for(int i=1;i<=m;i++)
        if(f[pr[i]]==M) ans+=pr[i];
    printf("%lld\n",ans);

}
```
