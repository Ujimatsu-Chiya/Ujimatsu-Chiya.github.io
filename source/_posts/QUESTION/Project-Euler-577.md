---
title: Project Euler 577
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-13 22:57:07
---

<escape><!-- more --></escape>

# Project Euler 577

## 题目

### Counting hexagons

An equilateral triangle with integer side length $n \ge 3$ is divided into $n^2$ equilateral triangles with side length $1$ as shown in the diagram below.

The vertices of these triangles constitute a triangular lattice with $\dfrac{(n+1)(n+2)} 2$ lattice points.

Let $H(n)$ be the number of all regular hexagons that can be found by connecting $6$ of these points.

![](../images/p577_counting_hexagons.png)

For example, $H(3)=1$, $H(6)=12$ and $H(20)=966$.

Find $\displaystyle \sum_{n=3}^{12345} H(n)$.

## 解决方案

通过容斥原理，不难写成$H(n)=3H(n-1)-3H(n-2)+H(n-3)+F(n)$，其中$F(n)$是**恰好**能够镶嵌在边长为$n$的正三角形上的正六边形个数。

并且，这些正六边形都只能镶嵌在边长为$3$的倍数的等边三角形上，如图：

![](../images/p577-1.png)

这是$n=9$种不同时的情况，$3$种颜色分别代表$3$个镶嵌的三角形。那么，当$n\%3=0$时，$F(n)=\dfrac{n}{3}$，否则$F(n)=0.$

为了使得正六边形是镶嵌在边长为$n$的三角形中，那么这个正六边形中的六个顶点，逆时针顺序间隔的三个顶点分别在三角形的三条边上。假设间隔开的这三个顶点为$D,E,F$，原来的等边三角形三个顶点为$A,B,C$，那么必有$AD=BE=CF.$，然后等边三角形$DEF$每条边再向外扩展出一个顶角为$120°$的等腰三角形，那么新的三个顶点和原来的三个顶点将会形成一个正六边形。最终不难输出可以进行扩展的数量为$\dfrac{n}{3}.$

通过上面的递推式，在oeis中查找到相关序列为[A011779](https://oeis.org/A011779)。并且在PROG一栏发现如下信息：

```
(PARI) a(n)=1/216 * n^4 + 1/12 * n^3 + 37/72 * n^2 + [5/4, 139/108, 131/108][1+n%3] * n + [1, 10/9, 7/9][1+n%3] \\ Yurii Ivanov, Jul 06 2021
```

这直接给出了这个数列的通项公式，直接实现即可。

## 代码

```py
N = 12345
ans = 0
for n in range(N - 2):
    ans += (n ** 4 + 18 * n ** 3 + 111 * n ** 2 + [270 * n + 216, 278 * n + 240, 262 * n + 168][n % 3]) // 216
print(ans)

```
