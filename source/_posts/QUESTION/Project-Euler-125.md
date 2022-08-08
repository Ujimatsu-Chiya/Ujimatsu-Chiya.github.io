---
title: Project Euler 125
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-06 22:24:53
---

<escape><!-- more --></escape>

# Project Euler 125

## 题目

### Palindromic sums

The palindromic number $595$ is interesting because it can be written as the sum of consecutive squares: $6^2 + 7^2 + 8^2 + 9^2 + 10^2 + 11^2 + 12^2$.

There are exactly eleven palindromes below one-thousand that can be written as consecutive square sums, and the sum of these palindromes is $4164$. Note that $1 = 0^2 + 1^2$ has not been included as this problem is concerned with the squares of positive integers.

Find the sum of all the numbers less than $10^8$ that are both palindromic and can be written as the sum of consecutive squares.

## 解决方案

先找出所有小于$N$的平方数，然后再找出一段段小于$N$的连续平方数之和。

由于每次枚举右端点时，连续平方数之和的是以立方级别增长。因此枚举一次左端点时，很快就结束了。

最终则把所有的回文连续平方数和插入集合中记录。

## 代码

```py
from tools import isqrt

N = 10 ** 8
a = [i * i for i in range(1, isqrt(N) + 1)]
st = set()
for i in range(len(a)):
    if i + 1 < len(a) and a[i] + a[i + 1] >= N:
        break
    s = a[i]
    for j in range(i + 1, len(a)):
        s += a[j]
        if s >= N:
            break
        t = str(s)
        if t == t[::-1]:
            st.add(s)
ans = sum(st)
print(ans)
```
