---
title: Project Euler 129
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 129
## 题目
### Repunit divisibility
A number consisting entirely of ones is called a repunit. We shall define $R(k)$ to be a repunit of length $k$; for example, $R(6) = 111111$.

Given that $n$ is a positive integer and $\gcd(n, 10) = 1$, it can be shown that there always exists a value, $k$, for which $R(k)$ is divisible by $n$, and let $A(n)$ be the least such value of $k$; for example, $A(7) = 6$ and $A(41) = 5$.

The least value of $n$ for which $A(n)$ first exceeds ten is $17$.

Find the least value of $n$ for which $A(n)$ first exceeds one-million.


## 解决方案

可以通过用等比数列数列求和将$R(k)$表示出来：

$$R(k)=\dfrac{10^k-1}{9}$$

如果$n|R(k)$，即$9n|(10^k-1)$，那么有$10^k-1\equiv 0 (\mod 9n)$，也就是$10^k\equiv 1(\mod 9n)$。那么，$A(n)$就是求最小的**正整数**$k$，以使得$k$满足以下方程：

$$10^k\equiv 1(\mod 9n)$$


## 代码


