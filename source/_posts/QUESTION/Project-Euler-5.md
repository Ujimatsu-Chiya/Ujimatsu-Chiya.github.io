---
title: Project Euler 5
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-26 18:35:16
---

<escape><!-- more --></escape>

# Project Euler 5

## 题目

### Smallest multiple

$2520$ is the smallest number that can be divided by each of the numbers from $1$ to $10$ without any remainder.

What is the smallest positive number that is *evenly divisible* by all of the numbers from $1$ to $20$?

## 解决方案

根据定义，所求的值为$1\sim20$中间的所有数的最小公倍数$\text{lcm}$。

求多个数的$\text{lcm}$和求多个数的最大公因数$\gcd$做法一样，都是两两按顺序求。

使用了`gmpy2`库中的`lcm`方法，以后将封装到`tools`工具包中。

## 代码

```Python
from gmpy2 import lcm

N = 20
ans = 1
for i in range(1, 21):
    ans = lcm(ans, i)
print(ans)

```
