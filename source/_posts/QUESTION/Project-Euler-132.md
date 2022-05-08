---
title: Project Euler 132
tags:
  - Project Euler
mathjax: true
date: 2022-05-08 11:56:06
---

<escape><!-- more --></escape>
  
# Project Euler 132

## 题目

### Large repunit factors

A number consisting entirely of ones is called a repunit. We shall define $R(k)$ to be a repunit of length $k$.

For example, $R(10) = 1111111111 = 11×41×271×9091$, and the sum of these prime factors is $9414$.

Find the sum of the first forty prime factors of $R(10^9)$.

## 解决方案

可以通过用等比数列数列求和将$R(k)$表示出来：

$$R(k)=\dfrac{10^k-1}{9}$$

如果质数$p$满足$p|R(k)$，即$9p|(10^k-1)$，那么有$10^k-1\equiv 0 (\mod 9p)$，也就是$10^k\equiv 1(\mod 9p)$。

质数$3$则进行特判。对于大于$5$的质数，如果$p|R(k)$，那么$p|10^k-1$。因此，可以通过[费马小定理](https://mathworld.wolfram.com/FermatsLittleTheorem.html)加速判断$10^k\equiv 1(\mod p)$是否满足。

直接从小到大判断所有质数是否可行。

当质数$p$大于$5$时，还有另外一种判断方式：元素$10$在乘法群$Z_p^*$的阶$\lambda_{p}(10)$是否为$10^9$的因数。

## 代码

```py
from sympy import nextprime

N = 10 ** 9
Q = 40
a = []
if N % 3 == 0:
    a.append(3)
pr = 5
while len(a) < Q:
    pr = nextprime(pr)
    if pow(10, N % (pr - 1), pr) == 1:
        a.append(pr)
ans = sum(a)
print(ans)

```
