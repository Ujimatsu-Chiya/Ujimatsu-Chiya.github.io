---
title: Project Euler 609
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-13 21:21:14
---

<escape><!-- more --></escape>

# Project Euler 609

## 题目

### $\pi$ sequences

For every $n \ge 1$ the **prime-counting** function $\pi(n)$ is equal to the number of primes not exceeding $n$.

E.g. $\pi(6)=3$ and $\pi(100)=25$.

We say that a sequence of integers $u  = (u_0,\cdots,u_m)$ is a *$\pi$ sequence* if

- $u_n \ge 1$ for every $n$
- $u_{n+1}= \pi(u_n)$
- $u$ has two or more elements

For $u_0=10$ there are three distinct $\pi$ sequences: $(10,4),  (10,4,2)$ and $(10,4,2,1)$.

Let $c(u)$ be the number of elements of $u$ that are not prime.

Let $p(n,k)$ be the number of $\pi$ sequences $u$  for which $u_0\le n$ and $c(u)=k$.

Let $P(n)$ be the product of all $p(n,k)$ that are larger than $0$.

You are given: $P(10)=3\times8\times9\times3=648$ and $P(100)=31038676032$.

Find $P(10^8)$. Give your answer modulo $1000000007$.

## 解决方案

利用线性筛生成所有质数，并直接计算出函数$\pi$的值。$u$序列直接通过迭代$\pi$值产生。

注意到，对于相邻两个质数$p,q$，发现$\pi(p)=\pi(p+1)=\pi(p+2)=\dots=\pi(q-1)$。因此，同时处理开头为$p\sim q-1$的$u$序列。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=100000000;
const int M=4*log2(N+4);
int s[N+4];
int v[N+4],pr[N+4],m=0;
int cnt[M+4];
ll mod=1e9+7;
int main(){
    for(int i=2;i<=N;i++){
        if(v[i]==0) v[i]=i,pr[++m]=i;
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
        }
        s[i]=s[i-1]+(v[i]==i);
    }
    for(int i=1;i<=m;i++){
        int l=pr[i],r=(i==m?N:pr[i+1]-1);
        int c=0;
        for(int j=s[l];j;j=s[j]){
            if(v[j]!=j) ++c;
            cnt[c+1]+=r-l;
            ++cnt[c];
            if(j==1) break;
        }
    }
    ll ans=1;
    for(int j=0;j<=M;j++)
        if(cnt[j]>0) ans=ans*cnt[j]%mod;
    printf("%lld\n",ans);
}
```
