---
title: Project Euler 73
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-02 16:36:22
---

<escape><!-- more --></escape>

# Project Euler 73

## 题目

### Counting fractions in a range

Consider the fraction, $\dfrac{n}{d}$, where n and d are positive integers. If $n<d$ and $\gcd(n,d)=1$, it is called a reduced proper fraction.
If we list the set of reduced proper fractions for $d \leq 8$ in ascending order of size, we get:

$$\dfrac{1}{8},\dfrac{1}{7},\dfrac{1}{6},\dfrac{1}{5},\dfrac{1}{4},\dfrac{2}{7},\dfrac{1}{3},\mathbf{\dfrac{3}{8},\dfrac{2}{5},\dfrac{3}{7}},\dfrac{1}{2},\dfrac{4}{7},\dfrac{3}{5},\dfrac{5}{8},\dfrac{2}{3},\dfrac{5}{7},\dfrac{3}{4},\dfrac{4}{5},\dfrac{5}{6},\dfrac{6}{7},\dfrac{7}{8}$$

It can be seen that there are $3$ fractions between $\dfrac{1}{3}$ and $\dfrac{1}{2}$.

How many fractions lie between $\dfrac{1}{3}$ and $\dfrac{1}{2}$ in the sorted set of reduced proper fractions for $d \leq 12,000$?

## 解决方案

[Stern-Brocot Tree](https://en.wikipedia.org/wiki/Stern%E2%80%93Brocot_tree)，一种用来表示各种最简分数的数据结构，它的中序遍历结果就是Farey序列。

主要构造方式则是基于Farey的性质（第71题提过）：对于任意的Farey 序列$F_n$，其中任意连续的三个分数序列$\dfrac{x_1}{y_1},\dfrac{x_2}{y_2},\dfrac{x_3}{y_3}$，满足$\dfrac{x_2}{y_2}=\dfrac{x_1+x_3}{y_1+y_3}$。

本代码直接模拟遍历Stern-Brocot Tree，每一个节点就是一个分数的区间（也表示新生成的分数本身）。相比于直接暴力判断，优化了一个$\log$的级别。

遍历到分母大于$N=12000$就返回。

本题有线性或以下的做法，奈何本人水平有限，在此不详细提及。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N=12000;
const int lu=1,ld=3,ru=1,rd=2;
int ans=0;
void dfs(int lu,int ld,int ru,int rd){
    int mu=lu+ru,md=ld+rd;
    if(md>N) return;
    ++ans;
    dfs(lu,ld,mu,md);
    dfs(mu,md,ru,rd);
}
int main(){
    dfs(lu,ld,ru,rd);
    printf("%d\n",ans);
}

```
