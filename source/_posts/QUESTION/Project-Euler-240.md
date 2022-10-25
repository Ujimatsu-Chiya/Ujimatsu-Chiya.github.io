---
title: Project Euler 240
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-07-04 18:02:28
---

<escape><!-- more --></escape>

# Project Euler 240

## 题目

### Top Dice

There are $1111$ ways in which five $6$-sided dice (sides numbered $1$ to $6$) can be rolled so that the top three sum to $15$. Some examples are:

$\begin{aligned}
D_1,D_2,D_3,D_4,D_5 = 4,3,6,3,5\\
D_1,D_2,D_3,D_4,D_5 = 4,3,3,5,6\\
D_1,D_2,D_3,D_4,D_5 = 3,3,3,6,6\\
D_1,D_2,D_3,D_4,D_5 = 6,6,3,3,3
\end{aligned}$

In how many ways can twenty $12$-sided dice (sides numbered $1$ to $12$) be rolled so that the top ten sum to $70$?

## 解决方案

令$N=20,M=10,K=12,S=70$。考虑使用动态规划解决本题。

基本思想是：从小到大枚举需要添加的骰子。其中前$N-K$个不算和，只为后$K$个最大的算和。

假设状态$f(i,j,k,l)(0\le j\le i\le N,1\le k\le K,0\le l\le S)$表示满足以下条件的排列方案数：从小到大已经枚举了$i$个骰子，目前最大值为$k$，其中骰子$k$已经使用了$j$个，并且除去最小的不算数的那一部分，剩下的和为$l$。

这里采用的动态规划使用的是“我为人人”的方式，也就是考虑当前状态能够转移到哪些地方。

对于一个状态$f(i,j,k,l)$而言，它有以下转移方式：每次选择一个新的值$x$加入骰子序列，并且$x\ge k$：

当$x=k$时，有$f(i,j,k,l) \cdot\dfrac{i+1}{j+1}\rightarrow f(i+1,j+1,x,l+x\cdot [i\ge N-M]$.

当$x>k$时，有$f(i,j,k,l) \cdot(i+1)\rightarrow f(i+1,1,x,l+x\cdot [i\ge N-M]$.

其中，$f(i,j,k,l)$后面的那个系数是为了用于维护多重排列数。而$[]$表示示性函数，表示$[]$里面的值是否为真，如果为真，那么值为$1$，否则值为$0$.

那么，最终答案为：

$$\sum_{j=1}^N\sum_{k=1}^K f(N,j,k,S)$$

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=20,M=10,K=12,S=70;
ll f[N+4][N+4][K+4][S+4];
int main(){
    f[0][0][1][0]=1;
    for(int i=0;i<N;i++)
        for(int j=0;j<=i;j++)
            for(int k=1;k<=K;k++)
                for(int l=0;l<=S;l++){
                    if(f[i][j][k][l]==0) continue;
                    for(int x=k;x<=K;x++){
                        int ns=(i<N-M?l:l+x);
                        if(ns>S) continue;
                        int nj=(x==k?j+1:1);
                        f[i+1][nj][x][ns]+=f[i][j][k][l]*(i+1)/nj;
                    }
                }
    ll ans=0;
    for(int j=1;j<=N;j++)
        for(int k=1;k<=K;k++)
            ans+=f[N][j][k][S];
    printf("%lld\n",ans);

}

```
