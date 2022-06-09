---
title: Project Euler 56
tags:
  - Project Euler
mathjax: true
date: 2022-04-30 10:31:43
---

<escape><!-- more --></escape>

# Project Euler 56

## 题目

### Powerful digit sum

A googol ($10^{100}$) is a massive number: one followed by one-hundred zeros; $100^{100}$ is almost unimaginably large: one followed by two-hundred zeros. Despite their size, the sum of the digits in each number is only $1$.

Considering natural numbers of the form, $a^b$, where $a, b < 100$, what is the maximum digital sum?

## 解决方案

使用Python直接计算$a^b$的值，并计算出数位的和。

## 代码

```py
N = 100
ans = 0
for a in range(1, N):
    for b in range(1, N):
        ans = max(ans, sum(int(x) for x in str(a ** b)))
print(ans)
```
