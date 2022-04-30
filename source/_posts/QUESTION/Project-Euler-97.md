---
title: Project Euler 97
tags:
  - Project Euler
mathjax: true
date: 2022-04-30 10:33:00
---

<escape><!-- more --></escape>

# Project Euler 97

## 题目

### Large non-Mersenne prime

The first known prime found to exceed one million digits was discovered in $1999$, and is a Mersenne prime of the form $2^{6972593}−1$; it contains exactly $2,098,960$ digits. Subsequently other Mersenne primes, of the form $2^p−1$, have been found which contain more digits.

However, in $2004$ there was found a massive non-Mersenne prime which contains $2,357,207$ digits: $28433\times2^{7830457}+1$.

Find the last ten digits of this prime number.

## 解决方案

使用python中的pow直接计算。

## 代码

```Python
a = 7830457
b = 28433
mod = 10 ** 10
ans = (pow(2, a, mod) * b + 1) % mod
print("{:010}".format(ans))
```
