---
title: Project Euler 772
category:
  - Project Euler
tags:
  - OEIS
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 772
## 题目
### Balanceable $k$-bounded partitions


A $k$-bounded partition of a positive integer $N$ is a way of writing $N$ as a sum of positive integers not exceeding $k$.

A balanceable partition is a partition that can be further divided into two parts of equal sums.

For example, $3 + 2 + 2 + 2 + 2 + 1$ is a balanceable $3$-bounded partition of $12$ since $3 + 2 + 1 = 2 + 2 + 2$. Conversely, $3 + 3 + 3 + 1$ is a $3$-bounded partition of $10$ which is not balanceable.

Let $f(k)$ be the smallest positive integer $N$ all of whose $k$-bounded partitions are balanceable. For example, $f(3) = 12$ and $f(30) \equiv 179092994 \pmod {1\,000\,000\,007}$.

Find $f(10^8)$. Give your answer modulo $1\,000\,000\,007$.


## 解决方案

暴力枚举出$f$的前几项，在OEIS中查询得到结果为[A051426](https://oeis.org/A051426)。

标题直接给出$f(n)=\text{lcm}(2,4,6,\dots,n)=2\cdot\text{lcm}(1,2,3,\dots,n)$

那么为了计算$\text{lcm}(1,2,3,\dots,n)$，直接枚举出$n$以内的所有质数$p_i$，找到对应最大的$e_i$使得$p_i^{e_i}\le n$，直接相乘即可。


## 代码


```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=100000000;
const ll mod=1000000007;
int v[N+4],pr[N/5+1000],m=0;
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
    ll ans=2;
    for(int i=1;i<=m;i++){
        ll q=1;
        for(;q*pr[i]<=N;q*=pr[i]);
        ans=ans*q%mod;
    }
    printf("%lld\n",ans);
}


```