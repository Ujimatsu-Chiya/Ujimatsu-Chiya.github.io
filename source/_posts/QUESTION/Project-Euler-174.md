---
title: Project Euler 174
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-17 22:21:12
---

<escape><!-- more --></escape>

# Project Euler 174

## 题目

### Counting the number of “hollow” square laminae that can form one, two, three, … distinct arrangements

We shall define a square lamina to be a square outline with a square “hole” so that the shape possesses vertical and horizontal symmetry.

Given eight tiles it is possible to form a lamina in only one way: $3\times 3$ square with a $1\times1$ hole in the middle. However, using thirty-two tiles it is possible to form two distinct laminae.

![](../images/p173_square_laminas.gif)

If $t$ represents the number of tiles used, we shall say that $t = 8$ is type $L(1)$ and $t = 32$ is type $L(2)$.

Let $N(n)$ be the number of $t \le 1000000$ such that $t$ is type $L(n)$; for example, $N(15)$ = $832$.

What is $\sum N(n)$ for $1 \le n \le 10$?

## 解决方案

与173题一样，令$N=1000000$。假设内部的正方形边长为$a$，边框的宽度为$d$，那么大正方形的边长为$2d+a$，这个边框使用了$(2d+a)^2-a^2=4d(a+d)$个正方形。

计算出的式子有常数因子$4$，因此只需要$\dfrac{N}{4}$的空间。因此，直接枚举式子$a(a+d)$的值并统计即可。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
const int N=1000000,Q=10;
const int M=N/4;
int cnt[M+4];
int main(){
    for(int a=1;a+1<=M;a++)
        for(int d=1;d*(d+a)<=M;d++)
            ++cnt[d*(a+d)];
    int ans=0;
    for(int i=1;i<=M;i++)
        if(0<cnt[i]&&cnt[i]<=Q) ++ans;
    printf("%d\n",ans);
}

```
