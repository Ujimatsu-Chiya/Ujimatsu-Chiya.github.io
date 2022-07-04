---
title: Project Euler 239
tags:
  - Project Euler
mathjax: true
date: 2022-07-04 18:02:25
---

<escape><!-- more --></escape>

# Project Euler 239

## 题目

### Twenty-two Foolish Primes

A set of disks numbered $1$ through $100$ are placed in a line in random order.

What is the probability that we have a partial derangement such that exactly $22$ prime number discs are found away from their natural positions? (Any number of non-prime disks may also be found in or out of their natural positions.)

Give your answer rounded to $12$ places behind the decimal point in the form $0.abcdefghijkl$.

## 解决方案

令$N=100,O=22$，并且$N$以内一共有$M=25$个质数。

不难以下两个过程是独立的：

1. 从$M$个质数中选择$M-O$个，将它们放在原地，一共有$C_M^O$种方法。之后便不考虑这$M-O$个质数。
2. 这$O$个质数不应该在原地，但是剩下的$N-M$个非质数则随便排列。

考虑使用动态规划的思想解决第二个步骤的问题。令$f(i,j)(0\le j\le i)$表示有多少个长度为$i$的排列$p_1,p_2,p_3,\dots,p_{i-1},p_i$，对于特定的$j$个两两不同下标$a_1,a_2,\dots,a_j$（注意些下标是可以随意假设的，这里你可以假设成$a_i=i$），满足$p_{a_1}\neq a_1,p_{a_2}\neq a_2,\dots,p_{a_j}\neq a_j$.那么可以写出如下状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &i!  & & \mathrm{if\quad} j=0 \\
  &f(i,j-1)-f(i-1,j-1)& & \mathrm{else}
\end{aligned}\right.
$$

对于方程最后一行，$f(i-1,j-1)$中的每个排列$p_1,p_2,\dots,p_{i-1}$，都可以映射到$f(i,j-1)$中的$p_1,p_2,\dots,p_{i-1},\underline{i}$。在$f(i-1,j-1)$中的$j-1$个特定下标中，如果再加上一个$a_j=i$，那么就相当于在$f(i,j-1)$中去掉被$f(i-1,j-1)$映射出来的排列，剩下的就成为$f(i,j)$中的排列。

合并两个步骤，最终题目的答案为$\dfrac{C_M^O\cdot f(N-M+O,O)}{N!}$.

## 代码

```py
from tools import C

N = 100
M = 25
O = 22

fac = [1]
for i in range(1, N + 1):
    fac.append(fac[-1] * i)
f = [[0 for x in range(y + 1)] for y in range(N + 1)]  # A047920
for i in range(N + 1):
    f[i][0] = fac[i]
    for j in range(1, i + 1):
        f[i][j] = f[i][j - 1] - f[i - 1][j - 1]
ans = C(M, O) * f[N - (M - O)][O] / fac[N]
print("{:.12f}".format(ans))

```
