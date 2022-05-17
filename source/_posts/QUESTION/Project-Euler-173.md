---
title: Project Euler 173
tags:
  - Project Euler
mathjax: true
date: 2022-05-17 22:21:07
---

<escape><!-- more --></escape>

# Project Euler 173

## 题目

### Using up to one million tiles how many different “hollow” square laminae can be formed?

We shall define a square lamina to be a square outline with a square “hole” so that the shape possesses vertical and horizontal symmetry. For example, using exactly thirty-two square tiles we can form two different square laminae:

![](../images/p173_square_laminas.gif)

With one-hundred tiles, and not necessarily using all of the tiles at one time, it is possible to form forty-one different square laminae.

Using up to one million tiles how many different square laminae can be formed?

## 解决方案

令$N=10^6$。假设内部的正方形边长为$a$，边框的宽度为$d$，那么大正方形的边长为$2d+a$，这个边框使用了$(2d+a)^2-a^2=4d(a+d)$个正方形。

那么得到$4d(a+d)\le N$，有$a\le \dfrac{N}{4d}-d$。

因此，直接枚举$d$的值，就可以得到满足当前条件下的$a$的个数。

## 代码

```py
from itertools import count

N = 10 ** 6
M = N // 4
ans = 0
for d in count(1, 1):
    w = M // d - d
    if w < 0:
        break
    ans += w
print(ans)

```
