---
title: Project Euler 357
tags:
  - Project Euler
mathjax: true
date: 2022-06-02 21:03:46
---

<escape><!-- more --></escape>

# Project Euler 357

## 题目

### Prime generating integers

Consider the divisors of $30: 1,2,3,5,6,10,15,30$. It can be seen that for every divisor $d$ of $30$, $d+30/d$ is prime.

Find the sum of all positive integers $n$ not exceeding $100 000 000$ such that for every divisor $d$ of $n$, $d+n/d$ is prime.

## 解决方案

如果一个数$n$满足题目要求，那么$n$一定满足以下条件。

1. $n+1$一定是一个质数（因为每个数都有因子$1$，$n+1=\dfrac{n}{1}+1$
2. $n$是一个无平方因子数，如果存在一个质因子$p$，使得$p^2|n$，那么$p+(\dfrac{n}{p})=p\cdot(1+\dfrac{n}{p^2})$，那么此时的$p+\dfrac{n}{p}$不是质数。

对于剩下的所有数，直接枚举它们的因数，判断答案合法性即可。

## 代码

```C++
# include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=100000000;
int v[N+4],pr[N],m=0;
bool is_square_free[N+4];
bool ok(int x){
    for(int i=1;i*i<=x;i++)
    if(x%i==0){
        int w=i+x/i;
        if(v[w]!=w) return 0;
    }
    return 1;
}
int main(){
    for(int i=2;i<=N;i++){
        if(v[i]==0) v[i]=i,pr[++m]=i,is_square_free[i]=1;
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
            is_square_free[i*pr[j]]=(v[i]==pr[j]?0:is_square_free[i]);
        }
    }
    ll ans=1;
    for(int i=2;i<=m;i++){
        int x=pr[i]-1;
        if(is_square_free[x]&&ok(x)) ans+=x;
    }
    printf("%lld\n",ans);
}

```
