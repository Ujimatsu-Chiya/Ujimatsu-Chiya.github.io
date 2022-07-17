---
title: Project Euler 725
tags:
  - Project Euler
  - 动态规划
mathjax: true
date: 2022-07-17 23:11:54
---

<escape><!-- more --></escape>

# Project Euler 725

## 题目

### Digit sum numbers

A number where one digit is the sum of the **other** digits is called a *digit sum number* or DS-number for short. For example, $352, 3003$ and $32812$ are DS-numbers.

We define $S(n)$ to be the sum of all DS-numbers of $n$ digits or less.

You are given $S(3) = 63270$ and $S(7) = 85499991450$.

Find $S(2020)$. Give your answer modulo $10^{16}$.

## 解决方案

令$N=2020.$一个数如果是DS数，那么它的数位和是最大数位的$2$倍。这不难想到使用动态规划来做。

本题的动态规划过程考虑使用“我为人人”的方法，因为本质上都是对当前状态的所有数都添加一个新的数位$d$，从而到达下一个状态。

令状态$c(i,t,m)(1\le i\le N,0\le t\le18,0\le m\le9)$表示当前有多少个$i$位**有前导0**的数，其中数位之和为$t$，并且这$i$个数位中最大数位为$m.$

不难知道，对于初值$i=1,0\le j\le 9$，都有$c(i,j,j)=1.$

考虑对$c(i,t,m)$中的所有数后面都拼接一个新的数位$0\le d\le 9$，那么可以进行转移：

$c(i,t,m)\rightarrow c(i+1,t+d,\max(m,d))$

添加一个数位$d$后，那么数位和就变成了$t+d$，最大数位也变成了$\max(m,d).$

令状态$s(i,t,m)(1\le i\le N,0\le t\le18,0\le m\le9)$表示$i$位**有前导0**并满足以下条件的所有数之和：数位之和为$t$，并且这$i$个数位中最大数位为$m.$

同样不难知道，对于初值$i=1,0\le j\le 9$，都有$s(i,j,j)=j.$

考虑对$s(i,t,m)$中的所有数后面都拼接一个新的数位$0\le d\le 9$，那么可以进行转移：

$10s(i,t,m)+d\cdot c(i,t,m)\rightarrow s(i+1,t+d,\max(m,d))$

添加一个数位$d$后，相当于将$s(i,t,m)$中的所有数都乘$10$，并且每一个数都多了一个数位$d$，一共有$c(i,t,m)$个。

那么，题目最终所需要求的答案为：

$$\sum_{d=0}^9s(N,2d,d)$$

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=2020;
const int B=9,D=2*B;
ll mod=1e16;
ll c[N+1][D+1][B+1],s[N+1][D+1][B+1];
void add(ll &x,ll y){
    x=(x+y)%mod;
}
int main(){
    for(int j=0;j<=B;j++){
        c[1][j][j]=1;
        s[1][j][j]=j;
    }
    for(int i=1;i<N;i++)
        for(int t=0;t<=D;t++)
            for(int m=0;m<=B;m++)
                for(int d=0;d<=B&&t+d<=D;d++){
                    add(c[i+1][t+d][max(d,m)],c[i][t][m]);
                    add(s[i+1][t+d][max(d,m)],s[i][t][m]*10+c[i][t][m]*d);
                }
    ll ans=0;
    for(int j=0;j<=B;j++)
        add(ans,s[N][j+j][j]);
    printf("%lld\n",ans);
}

```
