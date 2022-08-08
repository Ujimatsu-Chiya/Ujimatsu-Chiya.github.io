---
title: Project Euler 20
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-27 09:55:54
---

<escape><!-- more --></escape>

# Project Euler 20

## 题目

### Factorial digit sum

$n!$ means $n \times (n − 1) \times \dots \times 3 \times 2 \times 1$.

For example, $10! = 10 \times 9 \times \dots \times 3 \times 2 \times 1 = 3628800$, and the sum of the digits in the number $10!$ is $3 + 6 + 2 + 8 + 8 + 0 + 0 = 27$.

Find the sum of the digits in the number $100!$.

## 解决方案

使用sympy库的factorial直接计算阶乘的值，之后将封装在tools自定义工具类中，以fac(n)的方式调用。

利用和第16题类似的方式求出其每个数位的和。

## 代码

```py
from sympy import factorial

N = 100
ans = sum(list(map(int, str(factorial(N)))))
print(ans)
```
