---
title: Project Euler 381
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-13 21:21:54
---


<escape><!-- more --></escape>

# Project Euler 381

## 题目

### (prime-k) factorial

For a prime $p$ let $S(p) = (\sum(p-k)!) \bmod(p)$ for $1 \le k \le 5$.

For example, if $p=7, (7-1)! + (7-2)! + (7-3)! + (7-4)! + (7-5)! = 6! + 5! + 4! + 3! + 2! = 720+120+24+6+2 = 872$.

As $872 \bmod(7) = 4, S(7) = 4$.

It can be verified that $\sum S(p) = 480$ for $5 \le p < 100$.

Find $\sum S(p)$ for $5 \le p < 10^8$.

## 威尔逊定理

[威尔逊定理](https://en.wikipedia.org/wiki/Wilson%27s_theorem)：一个数$p$为质数，当且仅当满足下面的条件：

$$(p-1)!\equiv-1 \pmod p$$

## 解决方案

假设已知$a=(p-5)!\%p$，那么有

$$\begin{aligned}
S(p)&=(a+(p-4)a+(p-4)(p-3)a+\dots+(p-4)(p-3)(p-2)(p-1)a) \% p\\
&=(a+(-4)a+(-4)(-3)a+\dots+(-4)(-3)(-2)(-1)a)\%p\\
&=9a \%p
\end{aligned}$$

那么接下来的问题是根据威尔逊计算$a$的值。

可以发现，$(p-1)\%p=(p-1)(p-2)(p-3)(p-4)a\%p=24a\%p$。

可以借助威尔逊定理，解出下面的式子，得到$a$的值。

$$24a\equiv -1\pmod p$$

为了避免扩展使用欧几里得算法的值，可以通过计算出$2,3$在$p$上的逆元，间接计算出$24$的逆元。

计算完成后，最终得到$S(p)=-9\cdot(24)^{-1}\% p$。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=1e8;
int pr[N+4],v[N+4],m=0;
int main(){
    for(int i=2;i<N;i++){
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
        if(p>=5){
            ll inv2=(p+1)>>1;
            ll inv3=(p%3==1?(p+p+1)/3:(p+1)/3);
            ans+=inv2*inv2%p*inv2%p*inv3%p*(p-1)%p*9%p;
        }
    }
    printf("%lld\n",ans);
}
```
