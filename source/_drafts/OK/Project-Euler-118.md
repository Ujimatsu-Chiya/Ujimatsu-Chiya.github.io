---
title: Project Euler 118
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 118
## 题目
### Pandigital prime sets


Using all of the digits $1$ through $9$ and concatenating them freely to form decimal integers, different sets can be formed. Interestingly with the set $\{2,5,47,89,631\}$, all of the elements belonging to it are prime.

How many distinct sets containing each of the digits one through nine exactly once contain only prime elements?

## 解决方案

由于这里每一个质数都只会占一部分的数位，因此需要统计

## 代码

```py
from itertools import permutations, combinations
from tools import is_prime

a = [1, 2, 3, 4, 5, 6, 7, 8, 9]
n = len(a)
cnt = [0 for i in range(1 << n)]
cnt[1 << (2 - 1)] = cnt[1 << (3 - 1)] = cnt[1 << (5 - 1)] = 1
for r in range(1, n + 1):
    for st in combinations(a, r):
        if sum(st) % 3 == 0:
            continue
        mask = 0
        for x in st:
            mask |= 1 << (x - 1)
        for per in permutations(st):
            if (per[-1] & 1) == 0 or per[-1] == 5:
                continue
            w = int("".join(str(x) for x in per))
            if is_prime(w):
                cnt[mask] += 1

f = [0 for i in range(1 << n)]
f[0] = 1
for i in range(1 << n):
    if cnt[i] > 0:
        for j in range(1 << n):
            if (j & i) == 0:
                f[i | j] += f[j] * cnt[i]

print(f[(1 << n) - 1])

```

