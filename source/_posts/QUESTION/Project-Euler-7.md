---
title: Project Euler 7
tags:
  - Project Euler
mathjax: true
date: 2022-04-26 18:35:22
---

<escape><!-- more --></escape>

# Project Euler 7

## 题目

### 10001st prime

By listing the first six prime numbers: $2, 3, 5, 7, 11$, and $13$, we can see that the $6\mathrm{th}$ prime is $13$.

What is the $10 001\mathrm{st}$ prime number?

## 解决方案

使用sympy库中的prime函数计算即可。筛选素数的常见筛法有线性筛（时间复杂度$O(n)$）和埃式筛。

## 代码

```Python
from sympy.ntheory.generate import prime

N = 10001
print(prime(N))
```

埃氏筛：

```Python
Q = 10001
pr = []
N = Q * len(bin(Q)) - 2
f = [0 for _ in range(N + 1)]
for i in range(2, N + 1):
    if f[i] == 0:
        pr.append(i)
        for j in range(i * i, N + 1, i):
            f[j] = 1

print(pr[Q - 1])
```
