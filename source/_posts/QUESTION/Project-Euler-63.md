---
title: Project Euler 63
tags:
  - Project Euler
mathjax: true
date: 2022-04-30 10:32:12
---

<escape><!-- more --></escape>

# Project Euler 63

## 题目

### Powerful digit counts

The $5$-digit number, $16807=7^5$, is also a fifth power. Similarly, the $9$-digit number, $134217728$=$8^9$, is a ninth power.

How many $n$-digit positive integers exist which are also an $n^{\th}$ power?

## 解决方案

可以发现，$10^n$是一个$n+1$位数。因此，如果一个数$a^n$为$n$位数，那么$a\leq 9$。

当$9^n$的位数小于$n$位时，统计结束。（因为$n$就算增加$1$，$9^n$再乘一个$9$，也没办法使积的位数增加多于$1$位，变成$n+1$位）。

## 代码

```py
from itertools import count

ans = 0
for n in count(1, 1):
    if len(str(9 ** n)) < n:
        break
    for a in range(1, 10):
        if len(str(a ** n)) == n:
            ans += 1
print(ans)

```
