---
title: Project Euler 485
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-22 23:26:56
---

<escape><!-- more --></escape>

# Project Euler 485

## 题目

### Maximum number of divisors

Let $d(n)$ be the number of divisors of $n$.

Let $M(n,k)$ be the maximum value of $d(j)$ for $n \le j \le n+k-1$.

Let $S(u,k)$ be the sum of $M(n,k)$ for $1 \le n \le u-k+1$.

You are given that $S(1000,10)=17176$.

Find $S(100 000 000,100 000)$.

## 单调队列

单调队列是一种数据结构，通常用于维护区间的最值。

通常解决的问题是，给定一系列的区间$[l_1,r_1],[l_2,r_2],[l_3,r_3],\dots$的询问，分别求这些区间的最值。而且，$l_1\le l_2\le l_3\le \dots,r_1\le r_2\le r_3\le \dots$，即询问的$l_i,r_i$是不递减的。

那么考虑维护一个队列。一开始，询问的元素都被推进队列中，随着整个程序的运行，序列前面的元素已经过时，不再被询问，被弹出队列；而后面需要被询问的元素逐渐被推入队列中。但是，推入的新元素可能**比旧元素更优**，那么此时旧元素原地退出队列，让位给新元素，整个过程将会保持队列的单调性。队头的元素最优，队尾的元素最劣。

## 解决方案

$$S(N,K)=\sum_{i=1}^{N-K+1} \max_{j=i}^{i+K-1} \{d(j)\}$$

那么，询问值将是$[1,K],[2,K+1],[3,K+2],\dots$因此，使用单调队列来维护这些询问值。最终将每次维护结果的队头相加即可。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=100000000,K=100000;
int f[N+4],v[N+4],pr[N/10+100],m=0;
int main(){
    f[1]=1;
    for(int i=2;i<=N;i++){
        if(v[i]==0) pr[++m]=i,v[i]=i,f[i]=2;
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
            f[i*pr[j]]=(v[i]==pr[j]?f[i]*2-f[i/pr[j]]:f[i]*2);
        }
    }
    ll ans=0;
    deque<int>q;
    for(int i=K,j=1;i<=N;i++){
        while(!q.empty()&&i-q.front()>=K) q.pop_front();
        for(;j<=i;j++){
            while(!q.empty()&&f[j]>=f[q.back()]) q.pop_back();
            q.push_back(j);
        }
        ans+=f[q.front()];
    }
    printf("%lld\n",ans);
}
```
