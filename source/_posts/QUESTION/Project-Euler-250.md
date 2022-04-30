---
title: Project Euler 250
tags:
  - Project Euler
  - 动态规划
mathjax: true
date: 2022-04-30 10:31:04
---


<escape><!-- more --></escape>

# Project Euler 250

## 题目

### 250250

Find the number of non-empty subsets of $\{1^1, 2^2, 3^3,\dots, 250250^{250250}\}$, the sum of whose elements is divisible by $250$. Enter the rightmost $16$ digits as your answer.

## 解决方案

假设$n=250250,m=250$
题目可以转化为：在这$2^{n}-1$个非空子集中，有多少个的子集的和模$m$的值为$0$？

记录状态$f(i,j)(0\leq i\leq n,0\leq j< m)$为：当前使用了前$i$个数的情况下，有多少个子集的和对$m$取模为$j$.

对于第$i$个数$x=i^i$而言，有两种决策：取或者是不取。
如果取，就是从$f(i-1,(j-x) \% m)$转移而来。因为加了这一个数后，集合中所有的数和取模都变成了$j$。
如果不取，那么直接保留上一次的结果，即$f(i-1,j)$。

一开始什么数都不取的时候（空集），总和为$0$。最后需要减去空集的情况。

最终可以写出状态转移方程如下：

$$
f(i,j)= 
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=0\&j=0 \\
  &0 & & \mathrm{else if\quad} i=0 \\
  &f(i-1,j) + f(i-1,(j-i^i) \% m) & & \mathrm{else}
\end{aligned}\right.
$$

求得的答案为$f(n,0)-1$。

## 代码
```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=250250;
const int M=250;
ll mod=1e16;
ll qpow(ll n,ll m,ll mod){
    ll a=1;
    for(;m;m>>=1){
        if(m&1) a=a*n%mod;
        n=n*n%mod;
    }
    return a;
}
ll f[2][M],c[M];
int main(){
    f[0][0]=1;
    for(int i=1,p=1;i<=N;i++,p^=1){
        int x=qpow(i,i,M);
        ++c[x];
        for(int j=0;j<M;j++){
            f[p][j]=f[p^1][j]+f[p^1][(j-x+M)%M];
            if(f[p][j]>=mod) f[p][j]-=mod;
        }
    }
    printf("%016lld\n",(f[N&1][0]-1+mod)%mod);
}
```