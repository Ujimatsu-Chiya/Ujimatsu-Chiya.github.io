---
title: Project Euler 5
tags:
  - Project Euler
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

根据定义，所求的值为$1\sim20$中间的所有数的最小公倍数lcm。

求多个数的lcm和求多个数的最大公因数gcd做法一样，都是两两按顺序求。

使用了sympy库中的lcm，以后将封装到tools工具包中。

## 代码

```Python
from sympy import lcm
N = 20
ans = 1
for i in range(1, 21):
    ans = lcm(ans, i)
print(ans)
```
