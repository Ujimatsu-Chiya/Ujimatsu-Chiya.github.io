---
title: Project Euler 200
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-15 10:15:52
---

<escape><!-- more --></escape>

# Project Euler 200

## 题目

### Find the 200th prime-proof sqube containing the contiguous sub-string “200”

We shall define a sqube to be a number of the form, $p^2q^3$, where $p$ and $q$ are distinct primes.

For example, $200 = 5^2\times 2^3$ or $120072949 = 23^2\times 61^3$.
The first five squbes are $72, 108, 200, 392$, and $500$.

Interestingly, $200$ is also the first number for which you cannot change any single digit to make a prime; we shall call such numbers, prime-proof. The next prime-proof sqube which contains the contiguous sub-string "$200$" is $1992008$.

Find the $200\mathrm{th}$ prime-proof sqube containing the contiguous sub-string "$200$".

## 解决方案

令$Q=200$。由于本题所需要的质数上限比较难判定，所以使用的上限为$M=200000$。

从小到大枚举所有满足形如$p^2q^3$的数。本题通过之间产生的质数直接从小到大枚举。为保证每次枚举的值最小，使用了优先队列。

枚举时，为了避免枚举到$p=q$的情况，因此从一开始到整个的枚举过程，都需要保证$p< q$或者是$p>q$。此外，为了保证不重不漏，以$p< q$的情形为例：当$p=2$时，可以往右枚举$q$，也可以往下枚举$p$，但是，一旦$p$被枚举过，就不能再枚举$q$了。（枚举示意图如下）因为此时枚举$q$会导致大量的重复枚举，使程序运行很慢。

![](../images/p200-1.png)

基于$p^2q^3$变一位是否为质数，这个直接调用库的算法判定。

## 代码

```py
from tools import is_prime, get_prime
from queue import PriorityQueue

Q = 200
M = 200000


def judge(n: int):
    s = str(n)
    l = len(s)
    for i in range(l):
        d = int(s[i])
        for j in range(10):
            if i + j == 0 or d == j:
                continue
            x = int(s[:i] + str(j) + s[i + 1:])
            if is_prime(x):
                return False
    return True


q = PriorityQueue()
pr = get_prime(M)
q.put((pr[0] ** 2 * pr[1] ** 3, 0, 1))
q.put((pr[1] ** 2 * pr[0] ** 3, 1, 0))
cnt = 0
while True:
    w, x, y = q.get()
    if "200" in str(w) and judge(w):
        cnt += 1
        if cnt == Q:
            ans = w
            break
    if x + 1 != y and not (x > y and y != 0):
        q.put((pr[x + 1] ** 2 * pr[y] ** 3, x + 1, y))
    if x != y + 1 and not (x < y and x != 0):
        q.put((pr[x] ** 2 * pr[y + 1] ** 3, x, y + 1))

print(ans)

```
