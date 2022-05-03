---
title: Project Euler 94
tags:
  - Project Euler
  - 佩尔方程
mathjax: true
date: 2022-05-03 09:22:37
---

<escape><!-- more --></escape>

# Project Euler 94

## 题目

### Almost equilateral triangles

It is easily proved that no equilateral triangle exists with integral length sides and integral area. However, the almost equilateral triangle $5-5-6$ has an area of $12$ square units.

We shall define an almost equilateral triangle to be a triangle for which two sides are equal and the third differs by no more than one unit.

Find the sum of the perimeters of all almost equilateral triangles with integral side lengths and area and whose perimeters do not exceed one billion ($1,000,000,000$).

## 解决方案

![](../images/p094.png)

如上图，根据勾股定理，可以得到$a^2+4h^2=4b^2$。

又$a=b\pm1$，得$(b\pm1)+4h^2=4b^2$，

$3b^2-4h^2\pm 2b-1=0$，

$9b^2\pm 6b+1-12h^2=4$，

最终得到$(\dfrac{3b\pm1}{2})^2-3h^2=1$。

令$x=\dfrac{3b\pm1}{2},y=h$，即可得到佩尔方程$x^2-3y^2=1$。

因此，找到该佩尔方程的整数解后，还需判断$b=\dfrac{2x\pm 1}{3}$是否解出为整数。

使用66题中的解法，可以得到该佩尔方程的最小解为$(2,1)$。

那么，通解为$x_{k+1}=2x_k+3y_k,y_{k+1}=x_k+2y_k$。将值回代，计算出周长即可。

## 代码

```py
from tools import int_sqrt

N = 10 ** 9
ans = 0


def gen_solution():
    x, y = 2, 1
    yield x, y
    while True:
        x, y = 2 * x + 3 * y, x + 2 * y
        yield x, y


for x, h in gen_solution():
    if (2 * x + 1) % 3 == 0:
        b = (2 * x + 1) // 3
        a = int_sqrt(b * b - h * h) * 2
        C = a + b + b
        if C > N:
            break
        if min(a, b) > 0:
            ans += C

for x, h in gen_solution():
    if (2 * x - 1) % 3 == 0:
        b = (2 * x - 1) // 3
        a = int_sqrt(b * b - h * h) * 2
        C = a + b + b
        if C > N:
            break
        if min(a, b) > 0:
            ans += C

print(ans)

```
