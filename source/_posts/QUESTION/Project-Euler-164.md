---
title: Project Euler 164
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-05-15 10:15:44
---

<escape><!-- more --></escape>

# Project Euler 164

## 题目

### Numbers for which no three consecutive digits have a sum greater than a given value

How many $20$ digit numbers $n$ (without any leading zero) exist such that no three consecutive digits of $n$ have a sum greater than $9$?

## 解决方案

本题是一个明显的数位动态规划。

令$f(i,a,b)(i\ge 1,0\le a+b\le 9)$为目前符合题意的$i$位数中，个位为$b$，十位为$a$的数的个数，为了保证添加连续三个数的和不超过$9$，那么个位后面添加的数必须不超过$9-a-b$。

那么可以得到状态转移方程：

$$
f(i,a,b)=
\left \{\begin{aligned}
  &1  & & \text{if}\quad i=1\land a=0\land b>0 \\
  &0 & & \text{else if}\quad i=1 \\
  &\sum_{j=0}^{9-a-b} f(i-1,j,a) & & \text{else}
\end{aligned}\right.
$$

由于只有一位数时，十位为$0$，因此只要求$b>0$。而且，为了防止以后出现前导$0$，$f(1,0,0)=0$。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=20,M=10;
ll f[N+4][M][M];
int main(){
    for(int i=1;i<=9;i++)
        f[1][0][i]=1;
    for(int i=2;i<=N;i++)
        for(int a=0;a<=9;a++)
            for(int b=0;a+b<=9;b++)
                for(int j=0;a+b+j<=9;j++)
                    f[i][a][b]+=f[i-1][j][a];
    ll ans=0;
    for(int a=0;a<=9;a++)
        for(int b=0;a+b<=9;b++)
            ans+=f[N][a][b];
    printf("%lld\n",ans);
}

```
