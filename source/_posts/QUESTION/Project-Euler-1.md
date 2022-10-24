---
title: Project Euler 1
category:
  - Project Euler
tags:
  - 容斥原理
mathjax: true
date: 2022-04-24 13:38:00
---

<escape><!-- more --></escape>

# Project Euler 1

## 题目

### Multiples of $3$ or $5$

If we list all the natural numbers below $10$ that are multiples of $3$ or $5$, we get $3, 5, 6$ and $9$. The sum of these multiples is $23$.

Find the sum of all the multiples of $3$ or $5$ below $1000$.

## 解决方案

用容斥原理，先把$3$的倍数进行求和，再把$5$的倍数进行求和。加起来后，将$15$的倍数的总和减去即可。

## 代码

```Python
N = 1000
N -= 1
ans = 0
c3 = N // 3
c5 = N // 5
c15 = N // 15
ans = 3 * (c3 + 1) * c3 // 2 + 5 * (c5 + 1) * c5 // 2 - 15 * (c15 + 1) * c15 // 2
print(ans)
```
