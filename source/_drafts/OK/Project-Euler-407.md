---
title: Project Euler 407
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    


# Project Euler 407
## 题目
### Idempotents

If we calculate $a^2 \mod 6$ for $0 \le a \le 5$ we get: $0,1,4,3,4,1$.

The largest value of a such that $a^2 ≡ a \mod 6$ is $4$.

Let’s call $M(n)$ the largest value of $a < n$ such that $a^2 \equiv a (\mod n)$. So $M(6) = 4$.

Find $\sum M(n)$ for $1 \le n \le 10^7$.


## 解决方案

可以得到，$a(a-1)\equiv 0(\mod n)$。

由于$\gcd(a,a-1)=1$，假设$n$的分解质因数为$n=\prod_{i=1}^{k} p_i^{e_i}$，那么对于任意一个$p_i^{e_i}$，要么$p_i^{e_i}|a$，要么$p_i^{e_i}|(a-1)$。

那么枚举$n$的所有

## 代码


