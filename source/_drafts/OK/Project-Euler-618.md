---
title: Project Euler 618
tags:
  - Project Euler
mathjax: true
date: 2022-04-26 17:34:42
---

<escape><!-- more --></escape>

# Project Euler 618

## 题目

### Numbers with a given prime factor sum

Consider the numbers $15$, $16$ and $18$:

$15=3\times5$ and $3+5=8$. $16=2\times2\times2\times2$ and $2+2+2+2=8$.<br>$18=2\times3\times3$ and $2+3+3=8$. $15$, $16$ and $18$ are the only numbers that have $8$ as sum of the prime factors (counted with multiplicity).

We define $S(k)$ to be the sum of all numbers $n$ where the sum of the prime factors (with multiplicity) of $n$ is $k$. Hence $S(8)=15+16+18=49$.<br>Other examples: $S(1)=0$, $S(2)=2$, $S(3)=3$, $S(5)=5+6=11$.

The Fibonacci sequence is $F_1=1$, $F_2=1$, $F_3=2$, $F_4=3$, $F_5=5$, $\ldots$Find the last nine digits of $\sum_{k=2}^{24}S(F_k)$.

## 解决方案

本题使用动态规划（递推）思路解决，其阶段性特征比较明显。

设f(i,j)为使用了前i种质数，质因数之和为j的所有数的和。可以列出以下递推方程：

那么对于方程最后一行，有以下情况：

1. 直接把前只使用i-1素数的情况转移过来。
2. 把f(i,j-pr(i))中的所有数全部都添加一个质因数（也就是说，都乘一个pr(i)），就变成了f(i,j)的情况。由此，就能做到不重不漏的情况。
