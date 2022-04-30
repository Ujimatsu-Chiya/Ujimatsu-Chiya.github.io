---
title: Project Euler 52
tags:
  - Project Euler
mathjax: true
date: 2022-04-30 10:31:28
---

<escape><!-- more --></escape>

# Project Euler 52

## 题目

### Permuted multiples

It can be seen that the number, $125874$, and its double, $251748$, contain exactly the same digits, but in a different order.

Find the smallest positive integer, $x$, such that $2x, 3x, 4x, 5x,$ and $6x$, contain the same digits.

## 解决方案

直接枚举。可以发现，如果要满足上面的条件，那么$x$和$6x$的位数必须相同。

因此，对于一个$n$位数而言，只需要枚举这些$n$位数的前$\dfrac{1}{6}$的部分。

## 代码

```py
from itertools import count

for i in count(1, 1):
    l = 10 ** (i - 1)
    r = 10 ** i // 6
    ok = False
    for x in range(l, r + 1):
        st = set()
        for i in range(1, 7):
            st.add("".join((lambda x: (x.sort(), x)[1])(list(str(x * i)))))
        if len(st) == 1:
            ok = True
            ans = x
            break
    if ok:
        break
print(ans)
```
