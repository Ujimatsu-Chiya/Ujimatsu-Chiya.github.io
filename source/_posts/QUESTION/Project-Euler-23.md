---
title: Project Euler 23
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-27 09:56:07
---

<escape><!-- more --></escape>

# Project Euler 23

## 题目

### Non-abundant sums

A perfect number is a number for which the sum of its proper divisors is exactly equal to the number. For example, the sum of the proper divisors of $28$ would be $1 + 2 + 4 + 7 + 14 = 28$, which means that $28$ is a perfect number.

A number $n$ is called deficient if the sum of its proper divisors is less than $n$ and it is called abundant if this sum exceeds $n$.

As $12$ is the smallest abundant number, $1 + 2 + 3 + 4 + 6 = 16$, the smallest number that can be written as the sum of two abundant numbers is $24$. By mathematical analysis, it can be shown that all integers greater than $28123$ can be written as the sum of two abundant numbers. However, this upper limit cannot be reduced any further by analysis even though it is known that the greatest number that cannot be expressed as the sum of two abundant numbers is less than this limit.

Find the sum of all the positive integers which cannot be written as the sum of two abundant numbers.

## 解决方案

范围比较小，可以将所有的盈数处理出来，这里直接通过计算真因子和从而计算出来（也可以使用欧拉筛）。

枚举所有的盈数之和，并放进集合存储。

## 代码

```py
from tools import divisors_sigma


N = 28123
a = []
for i in range(1, N + 1):
    w = divisors_sigma(i)
    if w - i > i:
        a.append(i)

st = set()
for i in range(len(a)):
    for j in range(i, len(a)):
        if a[i] + a[j] > N:
            break
        st.add(a[i] + a[j])
ans = N * (N + 1) // 2 - sum(st)
print(ans)
```
