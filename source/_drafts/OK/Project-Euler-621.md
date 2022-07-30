---
title: Project Euler 621
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    


# Project Euler 621
## 题目
### Expressing an integer as the sum of triangular numbers

Gauss famously proved that every positive integer can be expressed as the sum of three **triangular numbers** (including $0$ as the lowest triangular number). In fact most numbers can be expressed as a sum of three triangular numbers in several ways.

Let $G(n)$ be the number of ways of expressing $n$ as the sum of three triangular numbers, regarding different arrangements of the terms of the sum as distinct.

For example, $G(9)=7$, as 9 can be expressed as: $3+3+3, 0+3+6, 0+6+3, 3+0+6, 3+6+0, 6+0+3, 6+3+0$.

You are given $G(1000)=78$ and $G(10^6)=2106$.

Find $G(17526\times10^9)$.


## 解决方案

令$n=\dfrac{a(a+1)}{2}+\dfrac{b(b+1)}{2}+\dfrac{c(c+1)}{2}$.

那么可以变形得：

$$8n+3=(2a+1)^2+(2b+1)^2+(2c+1)^2$$

令$r_3(n)$表示将一个数$n$写成$3$个奇数的平方的方法数，那么得$G(n)=r_3(8n+3)$。不难发现只有当$n$满足$n\equiv 3(\mod 8)$时，$r_3(n)>0$才成立。

这篇[论文](http://www.personal.psu.edu/jxs23/p7.pdf)给出了一个关于$r_3$的递推式：

$$r_3(9^\lambda n) =
\begin{cases}
3^\lambda \times r_3(n), & \text{if }n \equiv 11 \pmod{24} \\
(2\times3^\lambda -1) \times r_3(n) & \text{if } n \equiv 19 \pmod{24} \\
\dfrac{3^{\lambda+1}-1}{2} \times r_3(n) & \text{if } n \equiv 3 \text{ or } 51 \pmod{72}
\end{cases}$$

由于$17526\times 10^9\times 8+3=3^8 \times 13 \times 3527 \times 466073$。因此计算时我们仅需考虑去掉$9^{\lambda}$后的$n$。也就是$r(13 \times 3527 \times 466073)$。


## 代码


