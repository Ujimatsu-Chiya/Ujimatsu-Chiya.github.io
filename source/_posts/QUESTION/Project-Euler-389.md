---
title: Project Euler 389
category:
  - Project Euler
tags:
  - 概率
  - 动态规划
mathjax: true
date: 2022-07-12 00:16:50
---

<escape><!-- more --></escape>

# Project Euler 389

## 题目

### Platonic Dice

An unbiased single 4-sided die is thrown and its value, $T$, is noted.

$T$ unbiased $6$-sided dice are thrown and their scores are added together. The sum, $C$, is noted.

$C$ unbiased $8$-sided dice are thrown and their scores are added together. The sum, $O$, is noted.

$O$ unbiased $12$-sided dice are thrown and their scores are added together. The sum, $D$, is noted.

$D$ unbiased $20$-sided dice are thrown and their scores are added together. The sum, $I$, is noted.

Find the variance of $I$, and give your answer rounded to $4$ decimal places.

## 解决方案

不难想到使用动态规划解决本题。

当前先考虑一轮的过程：假设当前使用的是$m$面的骰子，那么令状态$g_m(i,j)(i,j\ge 0)$表示具有$i$个$m$面骰子的情况下，能够掷出$j$个点的概率。不难写出$g_m$的状态转移方程：

$$
g_m(i,j)=
\left \{\begin{aligned}
  &1  & & \text{if}\quad i=0 \\
  &\sum_{k=\max(j-m,0)}^{j-1}\dfrac{g_m(i-1,k)}{m} & & \text{else}
\end{aligned}\right.
$$

这个方程说明对于一个状态$f(i-1,k)$，它有$\dfrac{1}{m}$的概率转移到$g_m(i,k+1)$，也有$\dfrac{1}{m}$的概率转移到$g_m(i+1,k+2),\dots$

假设整个过程使用的骰子的面的序列为$d=\{4,6,8,12,20\}$，其中第$i$轮使用的骰子的面数为$d[i]$，令$N=5$为这个序列长度，$M=\prod_{k=1}^Nd_k$。令状态$f(i,j)(0\le i\le N,0\le j\le M)$在第$i$轮过后，投掷出$j$个点的概率。那么根据序列，不难写出状态转移方程为

$$
f(i,j)=
\left \{\begin{aligned}
  &1  & & \text{if}\quad i=0 \\
  &\sum_{k=1}^jf(i-1,k)\cdot g_{d[i]}(k,j) & & \text{else}
\end{aligned}\right.
$$

这个方程说明对于一个状态$f(i-1,k)$抛出了$k$个$d[i]$面的骰子后，会有$g_{d[i]}(k,j)$的概率抛出$j$面，从而转移到$f(i,j)$。

那么令$p(j)(0\le j\le M)=f(n,j)$，那么最终的变量$I$将会服从如$p$所示的分布。

为了计算随机变量$I$的方差$D[I]$，利用公式$D[I]=E[I^2]-E^2[I]$进行计算即可。

朴素实现一次$g_m(i,j)$的转移需要花费$O(m)$的时间复杂度。为了加速，我们注意到在实现$g_m$一个状态$g_m(i-1,j)$会**等概率**转移到下一个状态中的连续一段：$g(i,j+1),g(i,j+2),\dots,g(i,j+m)$，因此考虑使用一个差分数组$g'_m[i][j]$进行转移的保存：将$g'[i][j+1]$加上$\dfrac{g_m(i-1,j)}{m}$，将$g'[i][j+m+1]$减去$\dfrac{g_m(i-1,j)}{m}$。最终$g_m(i,j)=\sum_{k=1}^j g'[i][k]$就可以一次循环求出来，平均一个状态只有$O(1)$的时间复杂度。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
vector<int>d={4,6,8,12,20};
int main(){
    int m=1;
    vector<double>fp(2);
    fp[1]=1;
    for(int x:d){
        vector<double>gp(1,1);
        vector<double>fn(m*x+1,0);
        for(int i=1;i<=m;i++){
            vector<double>gn(x*i+1+1);
            for(int j=0;j<=x*(i-1);j++){
                gn[j+1]+=gp[j]/x;
                gn[j+x+1]-=gp[j]/x;
            }
            for(int j=1;j<=x*i;j++)
                gn[j]+=gn[j-1];
            gp=gn;
            for(int j=1;j<=x*i;j++)
                fn[j]+=fp[i]*gp[j];
        }
        fp=fn;
        m*=x;
    }
    double ex1=0,ex2=0;
    for(int i=1;i<=m;i++){
        ex1+=fp[i]*i;
        ex2+=fp[i]*i*i;
    }
    double ans=ex2-ex1*ex1;
    printf("%.4f\n",ans);
}

```
