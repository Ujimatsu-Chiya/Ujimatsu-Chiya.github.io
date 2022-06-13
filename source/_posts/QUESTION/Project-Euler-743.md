---
title: Project Euler 743
tags:
  - Project Euler
mathjax: true
date: 2022-06-13 21:21:30
---

<escape><!-- more --></escape>

# Project Euler 743

## 题目

### Window into a Matrix

A window into a matrix is a contiguous sub matrix.

Consider a $2\times n$ matrix where every entry is either $0$ or $1$.

Let $A(k,n)$ be the total number of these matrices such that the sum of the entries in every $2\times k$ window is $k$.

You are given that $A(3,9) = 560$ and $A(4,20) = 1060870$.

Find $A(10^8,10^{16})$. Give your answer modulo $1\,000\,000\,007$.

## 解决方案

本方案只适用于$k|n$的情况。

不难发现，对于$1\le i\le k$，第$i,i+k,i+2k,i+3k,\dots$列中，$1$的个数是相同的。

因此可以只考虑前$k$列的情况。

由于前$2\times k$个格子中，只有$k$个为$1$，因此最多只有$\lfloor\dfrac{k}{2}\rfloor$列是拥有两个$1$。剩下的$1$中，都被分配到了一个$1$的列。

枚举前$k$个格子中填充两个$1$的列的个数，那么答案为：

$$A(k,n)=\sum_{i=0}^{\lfloor\frac{k}{2}\rfloor}\frac{k!}{(n-2i)!(i!)^2}2^{\frac{n}{k}\cdot(k-2i)}$$

如果有$i$列有两个$1$，那么有$i$列没有$1$，有$k-2i$只有一个$1$。那么，$1$的分配方式就有$C_{k}^i\cdot C_{k-i}^i=\dfrac{k!}{(n-2i)!(i!)^2}$种。整个$2\times n$的格子中，有$\dfrac{n}{k}\cdot(k-2i)$列是只有一个$1$的，每一列有$2$种填法，由此得到$2^{\frac{n}{k}\cdot(k-2i)}$。最终通过组合得到上式。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const ll N = 1e16;
const ll K = 1e8;
const ll B = N/K;
ll mod=1e9+7;
ll qpow(ll n,ll m,ll mod){
    ll ans=1;
    for(;m;m>>=1){
        if(m&1) ans=ans*n%mod;
        n=n*n%mod;
    }
    return ans;
}
ll inv(ll n,ll p){
    return qpow(n,p-2,p);
}
int fac[K + 4],finv[K + 4];
int main(){
    fac[0]=fac[1]=1;
    finv[0]=1;
    for(int i=2; i <= K; i++)
        fac[i]=1ll*fac[i-1]*i%mod;
    finv[K]=inv(fac[K], mod);
    for(int i= K - 1; i > 0; i--)
        finv[i]=1ll*finv[i+1]*(i+1)%mod;
    ll pw2B=qpow(2,B,mod);
    ll invpw4B=inv(pw2B*pw2B%mod,mod);
    ll now=qpow(2,N,mod);
    ll ans=0;
    for(int i=0;i<=K/2;i++){
        ans=(ans+1ll*fac[K]*finv[K-2*i]%mod*finv[i]%mod*finv[i]%mod*now)%mod;
        now=now*invpw4B%mod;
    }
    printf("%lld\n",ans);
}

```
