---
title: Project Euler 549
tags:
  - Project Euler
mathjax: true
date: 2022-07-13 22:57:10
---

<escape><!-- more --></escape>

# Project Euler 549

## 题目

### Divisibility of factorials

The smallest number $m$ such that $10$ divides $m!$ is $m=5$.

The smallest number $m$ such that $25$ divides $m!$ is $m=10$.

Let $s(n)$ be the smallest number $m$ such that $n$ divides $m!$. So $s(10)=5$ and $s(25)=10$.

Let $S(n)$ be $\sum s(i)$ for $2 \le i \le n$. $S(100)=2012$.

Find $S(10^8)$.

## 解决方案

令$N=10^8.$

设$f(n, p)$是质因子$p$在$n!$中的次数，那么$f(n,p)=\lfloor\dfrac{n}{p}\rfloor+\lfloor\dfrac{n}{p^2}\rfloor+\lfloor\dfrac{n}{p^3}\rfloor+\dots$

令$n$的分解为$n=\prod_{i=1}^kp_i^{e_i}$，那么不难看出$s(n)$本质上是取决于$n$的分解中，每个$p_i^{e_i}$的分量的$s$函数值。也就是说，

$$s(n)=\max_{i=1}^ks(p_i^{e_i})$$

当求解$s(p_i^{e_i})$时，可以发现$e_i$其实很小，因此可以考虑从小到大枚举$p_i$的倍数$mp_i$，当$f(mp_i,p_i)\ge e_i$时，终止枚举，并且$s(p_i^{e_i})=mp_i.$

最终，通过筛法可以求出$N$以内的所有$s(n)$函数值。

本题似乎可以使用min_25筛法进行优化到亚线性级别的时间复杂度，待补。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=1e8;
int s[N+4];
int cals(int p,int e){
    ll k;
    for(k=p;;k+=p){
        ll t=k;
        for(;t%p==0&&e>0;--e,t/=p);
        if(e==0) break;
    }
    return k;
}
int main(){
    for(int i=2;i<=N;i++){
        if(s[i]!=0) continue;
        for(ll j=i,c=1;j<=N;j*=i,++c){
            int mx=cals(i,c);
            for(ll k=j;k<=N;k+=j)
                s[k]=max(s[k],mx);
        }
    }
    ll ans=0;
    for(int i=2;i<=N;i++){
        ans+=s[i];
    }
    printf("%lld\n",ans);
}

```
