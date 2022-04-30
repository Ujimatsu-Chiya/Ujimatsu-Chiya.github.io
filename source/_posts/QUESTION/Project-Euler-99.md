---
title: Project Euler 99
tags:
  - Project Euler
mathjax: true
date: 2022-04-27 23:33:02
---

<escape><!-- more --></escape>

# Project Euler 99

## 题目

### Largest exponential

Comparing two numbers written in index form like $2^{11}$ and $3^7$ is not difficult, as any calculator would confirm that $2^{11} = 2048 < 3^7 = 2187$.

However, confirming that $632382^{518061} > 519432^{525806}$ would be much more difficult, as both numbers contain over three million digits.

Using [base_exp.txt](./resources/p099_base_exp.txt) (right click and ‘Save Link/Target As…’), a 22K text file containing one thousand lines with a base/exponent pair on each line, determine which line number has the greatest numerical value.
NOTE: The first two lines in the file represent the numbers in the example given above.

## 解决方案

由于对数函数$y=\ln x$ 在 $(0,+\infty)$上递增。因此我们可以这些形如$a^b$的所有数全部取对数化成$b\ln a$，它们的相对大小依然不变。

因此，直接将所有数的对数值计算出即可完成比较。

## 代码

```py
from math import log

ls = open('p099_base_exp.txt', 'r').readlines()
ans, i, mx = 0, 0, 0
for s in ls:
    i += 1
    s = s[:-1]
    p, e = [int(x) for x in s.split(',')]
    w = log(p) * e
    if w > mx:
        mx = w
        ans = i
print(ans)
```
