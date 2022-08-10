---
title: Project Euler 618
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-04-26 17:34:42
---


<escape><!-- more --></escape>

# Project Euler 618

## 题目

### Numbers with a given prime factor sum

Consider the numbers $15$, $16$ and $18$:

$15=3\times5$ and $3+5=8$. $16=2\times2\times2\times2$ and $2+2+2+2=8$.

$18=2\times3\times3$ and $2+3+3=8$. $15$, $16$ and $18$ are the only numbers that have $8$ as sum of the prime factors (counted with multiplicity).

We define $S(k)$ to be the sum of all numbers $n$ where the sum of the prime factors (with multiplicity) of $n$ is $k$. Hence $S(8)=15+16+18=49$.

Other examples: $S(1)=0$, $S(2)=2$, $S(3)=3$, $S(5)=5+6=11$.

The Fibonacci sequence is $F_1=1$, $F_2=1$, $F_3=2$, $F_4=3$, $F_5=5$, $\ldots$Find the last nine digits of $\sum_{k=2}^{24}S(F_k)$.

## 解决方案

本题使用动态规划（递推）思路解决，其阶段性特征比较明显。

设$p$为存放质数的数组，$f(i,j)(i,j\geq 0)$为使用了前$i$种质数，质因数之和为$j$的所有数的和。可以列出以下递推方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &1  & & \text{if\quad} j=0 \\
  &0 & & \text{else if\quad} i=0 \\
  &f(i-1,j) & & \text{else if\quad} j<p[j] \\
  &f(i-1,j)+f(i,j-p[i])\times p[i] & & \text{else}
\end{aligned}\right.
$$

那么对于方程最后一行，有以下情况：

1. 直接把前只使用$i-1$素数的情况转移过来。
2. 把$f(i,j-p[i])$中的所有数全部都添加一个质因数（也就是说，都乘一个$p[i]$），就变成了$f(i,j)$的情况，由此就能做到不重不漏的情况。

将$F_{24}$以内的质数预处理出来，假设有$m$个。那么答案为$\sum_{k=2}^{24} f(m,F_k)$。

## 代码

```C++
# include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=100000,Q=24;
bool b[N+4];
int pr[N+4],m=0;
int que[144],p=0;
ll f[N+4],mod=1e9;
int main(){
    for(int i=1,a=1,b=2;i<Q;i++){
        que[++p]=a;
        int c=a+b;
        a=b;b=c;
    }
    int mx=que[p];
    for(int i=2;i<=mx;i++){
        if(b[i]) continue;
        pr[++m]=i;
        for(int j=i+i;j<=mx;j+=i)
            b[j]=1;
    }
    f[0]=1;
    for(int i=1;i<=m;i++)
        for(int j=pr[i];j<=mx;j++)
            f[j]=(f[j]+f[j-pr[i]]*pr[i])%mod;
    ll ans=0;
    for(int i=1;i<=p;i++)
        ans=(ans+f[que[i]])%mod;
    printf("%lld\n",ans);
}

```
