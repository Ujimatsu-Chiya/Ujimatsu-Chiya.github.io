---
title: Project Euler 226
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-05 09:28:40
---

<escape><!-- more --></escape>

# Project Euler 226

## 题目

### A Scoop of Blancmange

The *blancmange curve* is the set of points $(x, y)$ such that $0 \le x \le 1$ and $y = \sum \limits_{n = 0}^{\infty} {\dfrac{s(2^n x)}{2^n}}$, where $s(x)$ is the distance from $x$ to the nearest integer.

The area under the blancmange curve is equal to $\dfrac{1}{2}$, shown in pink in the diagram below.

![](../images/p226_scoop2.gif)

Let $C$ be the circle with centre $(\dfrac{1}{4},\dfrac{1}{2})$ and radius $\dfrac{1}{4}$, shown in black in the diagram.

What area under the blancmange curve is enclosed by $C$?

Give your answer rounded to eight decimal places in the form $0.abcdefgh$

## 解决方案

该[页面](https://en.wikipedia.org/wiki/Blancmange_curve#Integrating_the_Blancmange_curve)给出了求解牛奶冻曲线积分的递推公式。如果$f(x)=\sum \limits_{n = 0}^{\infty} {\dfrac{s(2^n x)}{2^n}}$，那么有$I(x)$：

$$I(x)=\int_{0}^x f(x)dx=
\left \{\begin{aligned}
  &\dfrac{I(2x)}{4}+\dfrac{x^2}{2}  & & \mathrm{if\quad} 0\le x\le \dfrac{1}{2} \\
  &\dfrac{1}{2}-I(1-x)  & & \mathrm{if\quad} \dfrac{1}{2}\le x\le 1 \\
  &\dfrac{n}{2}+I(x-n)  & & \mathrm{if\quad} n\le x\le(n+1) \\
\end{aligned}\right.
$$

为方便计算，我们假设圆$C$和曲线中只有两个交点，其中右交点在$B(0.5,f(0.5))$，左交点通过二分法来求出，假设为为$A(a,f(a))$。

接下来使用该[页面](https://en.wikipedia.org/wiki/Circular_segment)的一些公式计算了弓形$\mathop{AB}\limits^{\frown}$的面积，从而计算出弧$\mathop{AB}\limits^{\frown}$竖直向下的那一块面积$S$，也就是说，

$$S=\int_a^{\frac{1}{2}} \frac{1}{2} - \sqrt{\frac{1}{4}^2 - \left(x - \frac{1}{2}\right)^2}dx$$

最终答案为$I(\dfrac{1}{2})-I(a)-S$。

## 代码

```py
from math import asin, sin

f = lambda x: sum(abs(x * (1 << n) - round(x * (1 << n))) / (1 << n) for n in range(60))
g = lambda x: 0.5 - (x / 2 - x * x) ** 0.5


def I(x):
    if x < 1e-13:
        return 0
    if x <= 0.5:
        return I(2 * x) / 4 + x * x / 2
    else:
        return 0.5 - I(1 - x)


l, r = 0, 0.5
for _ in range(100):
    mid = (l + r) * 0.5
    if f(mid) > g(mid):
        r = mid
    else:
        l = mid
xl, xr = l, 0.5
yl, yr = g(xl), g(xr)
cr = 1 / 4
d = ((xl - xr) ** 2 + (yl - yr) ** 2) ** 0.5
theta = 2 * asin(d / (2 * cr))
arc_area = cr * cr / 2 * (theta - sin(theta))
circle_integral = (yl + yr) * (xr - xl) / 2 - arc_area
ans = I(xr) - I(xl) - circle_integral
print("{:.8f}".format(ans))

```
