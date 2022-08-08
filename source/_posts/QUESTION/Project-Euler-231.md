---
title: Project Euler 231
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-30 20:27:57
---

<escape><!-- more --></escape>

# Project Euler 231

## 题目

### The prime factorisation of binomial coefficients

The binomial coefficient $\displaystyle \binom {10} 3 = 120$.

$120 = 2^3 \times 3 \times 5 = 2 \times 2 \times 2 \times 3 \times 5$, and $2 + 2 + 2 + 3 + 5 = 14$.

So the sum of the terms in the prime factorisation of $\displaystyle \binom {10} 3$ is $14$.

Find the sum of the terms in the prime factorisation of $\displaystyle \binom {20\,000\,000} {15\,000\,000}$.

## 解决方案

组合数$C_n^m$的定义为$\dfrac{n!}{(n-m)!m!}$。因此，求一个质因数$p$在组合数的次数，本质上是求在阶乘中出现的次数。

设$f(n, p)$是质因子$p$在$n!$中的次数，那么$f(n,p)=\lfloor\dfrac{n}{p}\rfloor+\lfloor\dfrac{n}{p^2}\rfloor+\lfloor\dfrac{n}{p^3}\rfloor+\dots$，每一项分别表示$1\sim n$中有多少个数是$p,p^2,p^3\dots$的倍数。

因此根据组合数的定义式，质因子$p$出现的次数为$f(n,p)-f(m,p)-f(n-m,p)$。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=20000000,M=15000000;
int v[N+4],pr[N/10],m=0;
ll f(ll n,ll p){
    ll ans=0;
    for(;n;n/=p)
        ans+=n/p;
    return ans;
}
int main(){
    for(int i=2;i<=N;i++){
        if(v[i]==0){
            v[i]=i;pr[++m]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
        }
    }
    ll ans=0;
    for(int i=1;i<=m;i++){
        int p=pr[i];
        ans+=(f(N,p)-f(M,p)-f(N-M,p))*p;
    }
    printf("%lld\n",ans);
}

```
