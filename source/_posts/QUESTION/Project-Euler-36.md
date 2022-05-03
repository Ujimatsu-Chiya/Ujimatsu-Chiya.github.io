---
title: Project Euler 36
tags:
  - Project Euler
mathjax: true
date: 2022-04-27 23:32:18
---

<escape><!-- more --></escape>

# Project Euler 36

## 题目

### Double-base palindromes

The decimal number, $585 = 1001001001_2$ (binary), is palindromic in both bases.

Find the sum of all numbers, less than one million, which are palindromic in base $10$ and base $2$.

(Please note that the palindromic number, in either base, may not include leading zeros.)

## 解决方案

先枚举所有的二进制回文数，再判断其是否为十进制回文数。枚举的过程中，需要分开来考虑生成偶数长度的回文数和奇数长度的回文数。

这将只需要枚举$O(\sqrt N)$级别数量的数。

## 代码

```Python
N = 10 ** 6


def gen(n):
    s = bin(n)[2:]
    t = s[::-1]
    return int(s + t, 2), int(s + '0' + t, 2), int(s + '1' + t, 2)


M = int(N ** 0.5) + 4
ans = int(N > 1)
for i in range(1, M):
    ls = gen(i)
    for x in ls:
        s = str(x)
        if x < N and s == s[::-1]:
            ans += x
print(ans)
```
