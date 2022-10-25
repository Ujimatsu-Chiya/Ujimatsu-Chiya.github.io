---
title: Project Euler 793
category:
  - Project Euler
tags:
  - 二分
  - 双指针
mathjax: true
date: 2022-07-19 00:28:50
---

<escape><!-- more --></escape>

# Project Euler 793

## 题目

### Median of Products

Let $S_i$ be an integer sequence produced with the following pseudo-random number generator:

- $S_0 = 290797$
- $S_{i+1} = S_i ^2 \bmod 50515093$

Let $M(n)$ be the median of the pairwise products $ S_i S_j $ for $0 \le i \lt j \lt n$.

You are given $M(3) = 3878983057768$ and $M(103) = 492700616748525$.

Find $M(1\,000\,003)$.

## 解决方案

满足题意的中位数，本质上是求这$\dfrac{n(n+1)}{2}$个数中第$m=\left\lfloor\dfrac{n(n+1)+2}{4}\right\rfloor$小的数。

那么我们考虑二分法。二分答案$w$，然后统计小于等于$w$的数有多少个。如果大于等于$m$，那么说明这个数太大，否则说明这个数太小。第一个使得统计个数大于等于$m$的数就是答案。

先将将$S$中的前$n$项求出来后并排序，假设排序后的数组是$a_0,a_1,\dots,a_{n-1}$.

考虑当前对答案$w$进行判定，使用双指针法。左指针$l$从左到右遍历，右指针则逐渐向左移动，当$s[l]\cdot s[r]\le w$时停下。那么，$s[l]\cdot s[i],l< i\le r$这一段数都小于等于$w$，产生了$r-l$的贡献。最终，两个指针相遇时停止计算。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=1000003;
ll S[N+4],m=(1ll*N*(N-1)/2+1)>>1;
bool ok(ll x){
    ll ans=0;
    for(int l=0,r=N-1;l<N;l++){
        for(;r>=l&&S[l]*S[r]>x;r--);
        if(r<=l) break;
        ans+=r-l;
    }
    return ans>=m;
}
int main(){
    S[0]=290797;
    for(int i=1;i<N;i++)
        S[i]=S[i-1]*S[i-1]%50515093;
    sort(S,S+N);
    ll l=1,r=1ll*50515093*50515093;
    while(l<r){
        ll mid=(l+r)>>1;
        if(ok(mid)) r=mid;
        else l=mid+1;
    }
    printf("%lld\n",l);
}

```
