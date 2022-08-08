---
title: Project Euler 504
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-08 22:37:45
---

<escape><!-- more --></escape>

# Project Euler 504

## 题目

### Square on the Inside

Let $ABCD$ be a quadrilateral whose vertices are lattice points lying on the coordinate axes as follows:

$A(a, 0), B(0, b), C(-c, 0), D(0, -d)$, where $1 \le a, b, c, d \le m$ and $a, b, c, d, m$ are integers.

It can be shown that for $m = 4$ there are exactly $256$ valid ways to construct $ABCD$. Of these $256$ quadrilaterals, $42$ of them <u>strictly</u> contain a square number of lattice points.

How many quadrilaterals $ABCD$ strictly contain a square number of lattice points for $m = 100$?

## 皮克定理

[皮克定理](https://en.wikipedia.org/wiki/Pick%27s_theorem)：给定一个所有坐标点都在格点上的简单多边形。如果这个多边形的面积为$A$，边界上的格点有$b$个，内部的格点有$i$个。那么这三个变量满足关系：

$$A=i+\dfrac{b}{2}-1$$

## 解决方案

依靠皮克定理来解决问题。

不难计算出，这个多边形的面积为$\dfrac{(a+c)(b+d)}{2}$。

如果一条线段的两端的坐标分别在格点$(x_1,y_1),(x_2,y_2)$，那么在这些线段内部的格点有$\gcd(|x_1-x_2|,|y_1-y_2|)-1$个。

那么这个多边形内部的节点数为：

$\dfrac{(a+c)(b+d)-\gcd(a,b)-\gcd(b,c)-\gcd(c,d)-\gcd(d,a)-2}{2}$

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
const int N=100;
int g[N+1][N+1];
bool isq[N*N*4+1];
int main(){
    for(int i=1;i*i<=4*N*N;i++)
        isq[i*i]=1;
    for(int i=1;i<=N;i++)
        for(int j=1;j<=N;j++)
            g[i][j]=__gcd(i,j);
    int ans=0;
    for(int a=1;a<=N;a++)
        for(int b=1;b<=N;b++)
            for(int c=a;c<=N;c++)
                for(int d=b;d<=N;d++){
                    int v=((a+c)*(b+d)-(g[a][b]+g[b][c]+g[c][d]+g[d][a])+2)>>1;
                    if(isq[v]) ans+=(1+(a!=c))*(1+(b!=d));
                }
    printf("%d\n",ans);
}

```
