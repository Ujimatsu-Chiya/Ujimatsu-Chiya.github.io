---
title: Project Euler 187
category:
  - Project Euler
tags:
  - 双指针
mathjax: true
date: 2022-05-17 22:21:31
---

<escape><!-- more --></escape>

# Project Euler 187

## 题目

### Semiprimes

A composite is a number containing at least two prime factors. For example, $15 = 3 \times 5; 9 = 3 \times 3; 12 = 2 \times 2 \times 3$.

There are ten composites below thirty containing precisely two, not necessarily distinct, prime factors: $4, 6, 9, 10, 14, 15, 21, 22, 25, 26$.

How many composite integers, $n < 10^8$, have precisely two, not necessarily distinct, prime factors?

## 解决方案

由于要求的半素数其中一个质因子至少为$2$，因此只需要枚举$\dfrac{N}{2}$之前的质数。

由于$M=\dfrac{N}{2}$的范围依旧比较大，故使用线性筛将所有质数枚举出来。

按顺序产生质数后，设其数组为$pr$。使用双指针法，在第一层循环从左到右枚举左指针$l$，第二层循环右往左枚举右指针$r$，并枚举到第一个$pr[l]\cdot pr[r]< N$的最大$r$。$r$左边和$l$右边的所有质数都可以和$pr[l]$组成答案，统计这一段数的数量。

需要注意还有一种情况，就是质数的平方数。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int O=1e8;
const int N=O/2;
int v[N+4],pr[N+4],m=0;
int main(){
    for(int i=2;i<N;i++){
        if(v[i]==0){
            pr[++m]=i;v[i]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
        }
    }
    ll ans=0;
    for(int l=1,r=m;l<=r;l++){
        for(;pr[l]*pr[r]>=O;r--);
        ans+=r-l+1;
    }
    printf("%lld\n",ans);
}
```
