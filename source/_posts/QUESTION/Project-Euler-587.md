---
title: Project Euler 587
category:
  - Project Euler
tags:
  - 二分
mathjax: true
date: 2022-06-13 21:21:38
---

<escape><!-- more --></escape>

# Project Euler 587

## 题目

### Concave triangle

A square is drawn around a circle as shown in the diagram below on the left.
We shall call the blue shaded region the L-section.

A line is drawn from the bottom left of the square to the top right as shown in the diagram on the right.

We shall call the orange shaded region a concave triangle.

![](../images/p587_concave_triangle_1.png)

It should be clear that the concave triangle occupies exactly half of the L-section.

Two circles are placed next to each other horizontally, a rectangle is drawn around both circles, and a line is drawn from the bottom left to the top right as shown in the diagram below.

![](../images/p587_concave_triangle_2.png)

This time the concave triangle occupies approximately $36.46\%$ of the L-section.

If $n$ circles are placed next to each other horizontally, a rectangle is drawn around the $n$ circles, and a line is drawn from the bottom left to the top right, then it can be shown that the least value of $n$ for which the concave triangle occupies less than $10\%$ of the L-section is $n = 15$.

What is the least value of $n$ for which the concave triangle occupies less than $0.1\%$ of the L-section?

## 解决方案

这里假设每个圆的半径都为$1$。

不难计算出，原本的L-section面积为$S_0=1-\dfrac{\pi}{4}$。

假设题目中所求的圆的个数为$k$。以下图为例，此时的$k=3$。

![](../images/p587-3.png)

以$O$为原点，$OC$为$x$轴正方向建立平面直角坐标系，那么$\odot P$的方程为$(x-1)^2+(y-1)^2=1$，$OB$为$y=\dfrac{x}{k}$。

联立$OB$和$\odot P$的方程，得到：

$$(k^2+1)x^2-2k(k+1)x+k^2=0$$

那么通过二次方程的求根公式，可以解出$A$的坐标。假设其为$(x_0,y_0)$。

那么凹三角形$OAC$就被直线$x=x_0$分成了两部分，一部分是左边的直角三角形，面积为$\dfrac{x_0y_0}{2}$。另一部分通过积分进行计算，面积为$I$，其中

$$\begin{aligned}
I&=\int_{x_0}^1 1-\sqrt{1-(x-1)^2}dx\\
&=\int_{x_0-1}^01-\sqrt{1-x^2}dx\\
&=\int_{0}^{1-x_0}1-\sqrt{1-x^2}dx\\
&=1-x_0-\int_{0}^{1-x_0}\sqrt{1-x^2}dx
\end{aligned}$$

经过查表，$\int \sqrt{1-x^2}dx=\dfrac{1}{2}(\arcsin x+x\sqrt{1-x^2})+C$

因此

$$I=1-x_0-\dfrac{1}{2}(\arcsin (1-x_0)+(1-x_0)\sqrt{1-(1-x_0)^2})$$

因此凹三角形$OAC$的总面积为

$$S_k=\dfrac{x_0y_0}{2}+1-x_0-\dfrac{1}{2}(\arcsin (1-x_0)+(1-x_0)\sqrt{1-(1-x_0)^2})$$

那么题目所求比例值为$\dfrac{S_k}{S_0}$。

随着$k$越大，值$\dfrac{S_k}{S_0}$越小，这个值具有**单调性**。为了找到符合题目要求的最小$k$，考虑使用[二分查找算法](https://en.wikipedia.org/wiki/Binary_search_algorithm)解决。

## 代码

```py
from math import pi, asin

R = 0.001
S0 = 1 - pi / 4
k = 1
l, r = 1, 10 ** 9
while l < r:
    k = (l + r) >> 1
    a = 1 + k * k
    b = -k * k * 2 - k * 2
    c = k * k
    d = b * b - 4 * a * c
    x = (-b - d ** 0.5) / (a * 2)
    t = 1 - x
    Sk = x * x / k / 2 + t - 0.5 * (asin(t) + t * (1 - t ** 2) ** 0.5)
    if Sk / S0 < R:
        r = k
    else:
        l = k + 1
ans = l
print(ans)

```
