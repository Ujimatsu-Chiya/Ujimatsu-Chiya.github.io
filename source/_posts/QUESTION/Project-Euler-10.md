---
title: Project Euler 10
tags:
  - Project Euler
mathjax: true
date: 2022-04-26 18:35:31
---

<escape><!-- more --></escape>

# Project Euler 10
## 题目
### Summation of primes

The sum of the primes below $10$ is $2 + 3 + 5 + 7 = 17$.
Find the sum of all the primes below two million.

## 解决方案

解法与第7题相同。不过此处使用的是sympy中sieve对象的方法primerange，用于生成小于N的所有素数。
该方法将会被封装在自定义的tools工具类中。

## 代码

```py
from sympy.ntheory.generate import sieve
N = 2 * 10 ** 6
ans = sum(list(sieve.primerange(N)))
print(ans)
```
埃氏筛：
```py
pr = []
N = 2000000
f = [0 for _ in range(N)]
f[0] = f[1] = 1

for i in range(2, N):
    if f[i] == 0:
        pr.append(i)
        for j in range(i * i, N, i):
            f[j] = 1
print(sum(pr))
```