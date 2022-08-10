---
title: Project Euler 178
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-05-19 21:56:53
---

<escape><!-- more --></escape>

# Project Euler 178

## 题目

### Step Numbers

Consider the number $45656$.

It can be seen that each pair of consecutive digits of $45656$ has a difference of one.

A number for which every pair of consecutive digits has a difference of one is called a step number.

A pandigital number contains every decimal digit from $0$ to $9$ at least once.

How many pandigital step numbers less than $10^{40}$ are there?

## 解决方案

本题是一道数位动态规划题。

在每一个符合题意的数后面，都有两种方案填上一个数（如果个位是$0$或者是$9$，那么后面只能填上一位）。另外，数位的使用情况肯定是连续的，因此可以由$2^{10}=1024$的状态空间优化成$55$种使用情况。

令$N=40$，那么令$f(i,l,r,d)(1\le i\le N,0\le l\le d\le r \le 9 )$为有多少个$i$位数，使用了$l$和$r$之间的数位，目前个位为$d$的数有多少个。那么可以列出如下状态转移方程：

$$
f(i,l,r,d)=
\left \{\begin{aligned}
  &1  & & \text{if\quad} i=1\land l=r\land r=d \\
  &0 & & \text{else if\quad} i=1\lor l=r\\
  &f(i-1,l,r,d+1)+f(i-1,l+1,r,d+1) & & \text{else if\quad} l=d \\
  &f(i-1,l,r,d-1)+f(i-1,l,r-1,d-1) & & \text{else if\quad} r=d \\
  &f(i-1,l,r,d+1)+f(i-1,l,r,d-1) & & \text{else}
\end{aligned}\right.
$$

对于第三行，如果新填的数是来自区间的最左边，那么它有可能是第一次用，从$f(i-1,l+1,r,d+1)$转移而来；也有可能是再次使用，从$f(i-1,l,r,d+1)$转移而来。第四行也类似。

对于最后一行，如果值在区间中间，那么它肯定不是第一次用，可以是之前填的数个位$-1$转移而来，也可以是$+1$转移而来。

最终答案为：

$$\sum_{i=1}^N\sum_{d=0}^9f(i,0,9,d)$$

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=40,M=10;
ll f[N+3][M][M][M];
int main(){
    for(int j=1;j<M;j++)
        f[1][j][j][j]=1;
    for(int i=2;i<=N;i++)
        for(int l=0;l<M;l++)
            for(int r=l;r<M;r++)
                for(int d=l;d<=r;d++){
                    if(l<d&&d<r) f[i][l][r][d]=f[i-1][l][r][d-1]+f[i-1][l][r][d+1];
                    else if(d==l) f[i][l][r][d]=f[i-1][l][r][d+1]+f[i-1][l+1][r][d+1];
                    else f[i][l][r][d]=f[i-1][l][r][d-1]+f[i-1][l][r-1][d-1];
                }
    ll ans=0;
    for(int i=1;i<=N;i++)
        for(int d=0;d<M;d++)
            ans+=f[i][0][9][d];
    printf("%lld\n",ans);
}

```
