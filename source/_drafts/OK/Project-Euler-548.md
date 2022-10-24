---
title: Project Euler 548
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>




# Project Euler 548
## 题目
### Gozinta Chains

A **gozinta chain** for $n$ is a sequence $\{1,a,b,\dots,n\}$ where each element properly divides the next.

There are eight gozinta chains for $12:$ 

$\{1,12\} ,\{1,2,12\}, \{1,2,4,12\}, \{1,2,6,12\}, \{1,3,12\}, \{1,3,6,12\}, \{1,4,12\}$ and $\{1,6,12\}$.

Let $g(n)$ be the number of gozinta chains for $n$, so $g(12)=8$. $g(48)=48$ and $g(120)=132$.

Find the sum of the numbers $n$ not exceeding $10^{16}$ for which $g(n)=n$.


## 解决方案

[A163272](https://oeis.org/A163272)

考虑以动态规划的思想求出$g(n)$。由于序列中每一项都是前一项的倍数。因此对于$g(d)$中的所有序列，假设$d$是$n$的因子，那么将$g(d)$所有序列的最后一项都乘上$\dfrac{n}{d}$，就可以得到$n$。因此不难写出$n$的状态转移方程：

$$
g(n)=
\left \{\begin{aligned}
  &1  & & \text{if}\quad n = 1 \lor n \in \Omega \\
  &\sum_{d\mid n,d<n} g(d) & & \text{else}
\end{aligned}\right.
$$



## 代码


