---
title: Project Euler 10
category:
  - Project Euler
tags:
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

解法与第7题相同。不过此处使用的是`sympy`中`sieve`对象的方法`primerange(l,r=None)`，只有一个参数$l$时，用于生成小于$l$的所有素数；有两个参数$l,r$时，生成的是$[l,r)$内的素数。

该方法将会被封装在自定义的`tools`工具类中，方法名为`get_prime`。

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
ans = sum(pr)
print(ans)
```
