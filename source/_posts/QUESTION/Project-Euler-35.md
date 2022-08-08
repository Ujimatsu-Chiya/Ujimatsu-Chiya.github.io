---
title: Project Euler 35
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-27 23:32:14
---

<escape><!-- more --></escape>

# Project Euler 35

## 题目

### Circular primes

The number, $197$, is called a circular prime because all rotations of the digits: $197, 971,$ and $719$, are themselves prime.

There are thirteen such primes below $100: 2, 3, 5, 7, 11, 13, 17, 31, 37, 71, 73, 79,$ and $97$.

How many circular primes are there below one million?

## 解决方法

除了$2$和$5$，容易知道，如果素数只要包含了数位$024568$，那么这些素数都不符合条件。因为经过循环移位后，这些数一定会变成$2$的倍数或者是$5$的倍数。

因此，仅需将剩下的这些数一个个进行枚举判断。
循环位移通过字符串直接进行操作。

## 代码

```py
from tools import get_prime

N = 10 ** 6
pr = set(x for x in get_prime(N) if all(c not in str(x) for c in "024568"))


def change(x: int):
    s = str(x)
    return int(s[-1] + s[:-1])


ans = int(N >= 2) + int(N >= 3)
for x in pr:
    m = len(str(x))
    ok = 1
    for i in range(m):
        if x not in pr:
            ok = 0
            break
        x = change(x)
    ans += ok
print(ans)
```
