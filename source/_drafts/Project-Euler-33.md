---
title: Project Euler 33
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 33
## 题目
### Digit cancelling fractions
The fraction $\dfrac{49}{98}$ is a curious fraction, as an inexperienced mathematician in attempting to simplify it may incorrectly believe that $\dfrac{49}{98}=\dfrac{4}{8}$, which is correct, is obtained by cancelling the $9$s.

We shall consider fractions like, $\dfrac{30}{50}=\dfrac{3}{5}$, to be trivial examples.

There are exactly four non-trivial examples of this type of fraction, less than one in value, and containing two digits in the numerator and denominator.

If the product of these four fractions is given in its lowest common terms, find the value of the denominator.
## 解决方案

所求解如果不是一个平凡解，那么，删除的位在分子和分母中一定不同，即有以下两种情况：

1. 删除分子的十位和分母的个位
2. 删除分子的个位和分母的十位

枚举分子和分母，判断这两种情况。

## 代码

```py
from tools import gcd

a, b = 1, 1
for x in range(10, 100):
    for y in range(x + 1, 100):
        ok = False
        u, v = x // 10, y % 10
        if x * v == y * u and x % 10 == y // 10:
            ok = True
        u, v = x % 10, y // 10
        if x * v == y * u and x // 10 == y % 10:
            ok = True
        if ok:
            a *= x
            b *= y
ans = b // gcd(a, b)
print(ans)
```