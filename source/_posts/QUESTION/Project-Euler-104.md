---
title: Project Euler 104
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:23:30
---

<escape><!-- more --></escape>

# Project Euler 104

## 题目

### Pandigital Fibonacci ends

The Fibonacci sequence is defined by the recurrence relation:

$F_n = F_n−1 + F_n−2$, where $F_1 = 1$ and $F_2 = 1$.

It turns out that $F_{541}$, which contains $113$ digits, is the first Fibonacci number for which the last nine digits are $1-9$ pandigital (contain all the digits $1$ to $9$, but not necessarily in order). And $F_{2749}$, which contains $575$ digits, is the first Fibonacci number for which the first nine digits are $1-9$ pandigital.

Given that $F_k$ is the first Fibonacci number for which the first nine digits AND the last nine digits are $1-9$ pandigital, find $k$.

## 解决方案

从小到大枚举斐波那契数的项数。由于本题只关心高$9$位和低$9$位，因此可以这么做：

1. 将整个数直接对$10^9$取模，那么所得到的值是精确的低$9$位。
2. 浮点数的特点是只保留前几位的有效数字，那么就用浮点数来存储整个值，只要前$9$位准确就行。

因此，计算低位时，只需要全程对$10^9$取模即可。

计算高位时，如果高位的数到达了一个阈值（这里设定为$10^{12}$），那么就对这个数除$10$。这不仅影响高位的准确性，还能在转字符串判断时，防止产生的浮点数字符串太长，加速判断。

## 代码

```py
from itertools import count

s = "123456789"
m = 10 ** len(s)
a = b = 1
u = v = 1.0

for i in count(1, 1):
    l = str(a)
    r = str(u)[:len(s)]
    l = "".join((lambda x: (x.sort(), x)[1])(list(l)))
    r = "".join((lambda x: (x.sort(), x)[1])(list(r)))
    if l == r == s:
        ans = i
        break
    a, b = b, (a + b) % m
    u, v = v, u + v
    if v > 1e12:
        u /= 10
        v /= 10
print(ans)

```
