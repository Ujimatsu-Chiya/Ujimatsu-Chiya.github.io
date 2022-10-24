---
title: Project Euler 34
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-27 23:32:10
---

<escape><!-- more --></escape>

# Project Euler 34

## 题目

### Digit factorials

$145$ is a curious number, as $1! + 4! + 5! = 1 + 24 + 120 = 145$.

Find the sum of all numbers which are equal to the sum of the factorial of their digits.

Note: as $1! = 1$ and $2! = 2$ are not sums they are not included.

## 解决方案

解法与30题相同。

一个$n$位数如果全是$9$，那么其和数位和的$k$次幂为$n\cdot 9!$。因此一个$n$位数的值绝不会超过$n \cdot 9!$。

如果$n$满足$10^n>n\cdot 9!$，那么停止循环退出。

## 代码

```py
from itertools import count

fac = [1]
for i in range(1, 10):
    fac.append(fac[-1] * i)
ans = 0
for n in count(1, 1):
    mx = min(10 ** (n + 1) - 1, n * fac[9])
    st = 10 ** n
    if st > n * fac[9]:
        break
    for i in range(st, mx + 1):
        s, w = 0, i
        while w:
            s += fac[w % 10]
            w //= 10
        if s == i:
            ans += i
print(ans)

```
