---
title: Project Euler 37
tags:
  - Project Euler
mathjax: true
date: 2022-04-27 23:32:22
---

<escape><!-- more --></escape>

# Project Euler 37

## 题目

### Truncatable primes

The number $3797$ has an interesting property. Being prime itself, it is possible to continuously remove digits from left to right, and remain prime at each stage: $3797, 797, 97,$ and $7$.

Similarly we can work from right to left: $3797$, $379$, $37$, and $3$.

Find the sum of the only eleven primes that are both truncatable from left to right and right to left.

NOTE: $2, 3, 5,$ and $7$ are not considered to be truncatable primes.

## 解决方案

和35题类似，如果素数的只要包含了数位$0468$，或者非最高位包含了$25$，那么这些素数都不符合条件。因为经过截断之后，这些数一定会变成$2$的倍数或者是$5$的倍数。

因此，仅需将剩下的这些数一个个进行枚举判断。

截断通过字符串直接进行操作。

## 代码

```py
from tools import get_prime

N = 1000000
pr = {x for x in {x for x in get_prime(N) if all(c not in str(x) for c in "0468")} if all(c not in str(x)[1:] for c in "25")}

ans = 0
for x in pr:
    if x < 10:
        continue
    s = str(x)
    m = len(s)
    ok = True
    for i in range(1, m):
        if int(s[:i]) not in pr or int(s[i:]) not in pr:
            ok = False
            break
    if ok:
        ans += x
print(ans)
```
