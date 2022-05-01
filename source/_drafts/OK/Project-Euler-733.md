---
title: Project Euler 733
tags:
  - Project Euler
mathjax: true
date: 2022-04-26 17:34:44
---

<escape><!-- more --></escape>

# Project Euler 733

## 题目

### Ascending subsequences

Let $a_i$ be the sequence defined by $a_i=153^i \bmod 10\ 000\ 019$ for $i \ge 1$. The first terms of $a_i$ are: $153, 23409, 3581577, 7980255, 976697, 9434375, \dots$

Consider the subsequences consisting of $4$ terms in ascending order. For the part of the sequence shown above, these are:$153, 23409, 3581577, 7980255\\153, 23409, 3581577, 9434375\\153, 23409, 7980255, 9434375\\153, 23409, 976697, 9434375\\153, 3581577, 7980255, 9434375\\23409, 3581577, 7980255, 9434375$.

Define $S(n)$ to be the sum of the terms for all such subsequences within the first $n$ terms of $a_i$. Thus $S(6)=94513710$. You are given that $S(100)=4465488724217$.

Find $S(10^6)$ modulo $1\ 000\ 000\ 007$.

## 解决方案

上升子序列问题一般是以动态规划为基本思想的问题。本题依旧尝试使用动态规划解决。

由于本题需要求的是所有严格上升子序列之和（而不是个数），因此需要维护多一个当前子序列的个数，再计算当前下标这个数的贡献次数。

因此，假设这个序列为$a$，其长度为$m$。设$c(i,j)(1\leq i\leq 4,1\leq j\leq m)$为长度为$i$的严格上升子序列中，第$i$个元素为$a[j]$的子序列有多少个。

可以列出以下状态转移方程：

$$
c(i,j)= 
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=1 \\
  &\sum_{1\leq k<j,a[k]<a[j]} c(i-1,k) & & \mathrm{else}
\end{aligned}\right.
$$

意思是，将之前所有末尾严格小于自身$a[j]$的子序列，末尾都添加一个$a[j]$，就变成了以$a[j]$为末尾的子序列。

再设$s(i,j)(1\leq i\leq 4,1\leq j\leq m)$为长度为$i$的严格上升子序列中，第$j$个元素为$a[j]$的所有子序列之和。

可以列出以下方程：

$$
s(i,j)= 
\left \{\begin{aligned}
  &a[j]  & & \mathrm{if\quad} i=1 \\
  &c(i,j)\times p[j]+\sum_{1\leq k<j,a[k]<a[j]} s(i-1,k) & & \mathrm{else}
\end{aligned}\right.
$$


需要注意，这个方程使用了上面的$c(i,j)$的值。

将之前所有末尾严格小于自身$a[j]$的子序列，由于末尾都添加一个$a[j]$，而子序列一共有$c(i,j)$个，因此总共的和添加了$c(i,j)\times p[j]$。


可以发现，直接按照方程进行计算的时间复杂度为$O(m^2)$，可以用树状数组进行优化。这里的用法则是将离散化后的数组值作为“键”，直接维护树状数组的值。

树状数组：一个可以用$O(\log m)$单次维护前缀和的一个数据结构。

最终答案为$\sum _{i=1}^m s(n,i)$。