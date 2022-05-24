---
title: Project Euler 465
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 465
## 题目
### Polar polygons

The <i>kernel</i> of a polygon is defined by the set of points from which the entire polygon's boundary is visible. We define a <i>polar polygon</i> as a polygon for which the origin is <u>strictly</u> contained inside its kernel.

For this problem, a polygon can have collinear consecutive vertices. However, a polygon still cannot have self-intersection and cannot have zero area.

For example, only the first of the following is a polar polygon (the kernels of the second, third, and fourth do not strictly contain the origin, and the fifth does not have a kernel at all):
<p align="center"><img src="project/images/p465_polygons.png" alt="p465_polygons.png" />


Notice that the first polygon has three consecutive collinear vertices.

Let P(<var>n</var>) be the number of polar polygons such that the vertices (<var>x</var>, <var>y</var>) have integer coordinates whose absolute values are not greater than <var>n</var>.

Note that polygons should be counted as different if they have different set of edges, even if they enclose the same area. For example, the polygon with vertices [(0,0),(0,3),(1,1),(3,0)] is distinct from the polygon with vertices [(0,0),(0,3),(1,1),(3,0),(1,0)].

For example, P(1) = 131, P(2) = 1648531, P(3) = 1099461296175 and P(343) mod 1 000 000 007 = 937293740.

Find P(7^13) mod 1 000 000 007.



# Project Euler 465
## 题目
### Polar polygons

The <em>kernel</em> of a polygon is defined by the set of points from which the entire polygon’s boundary is visible. We define a <em>polar polygon</em> as a polygon for which the origin is <u>strictly</u> contained inside its kernel.
For this problem, a polygon can have collinear consecutive vertices. However, a polygon still cannot have self-intersection and cannot have zero area.
For example, only the first of the following is a polar polygon (the kernels of the second, third, and fourth do not strictly contain the origin, and the fifth does not have a kernel at all):
<center><img src="https://projecteuler.net/project/images/p465_polygons.png"></center>

Notice that the first polygon has three consecutive collinear vertices.
Let P(n) be the number of polar polygons such that the vertices (x, y) have integer coordinates whose absolute values are not greater than n.
Note that polygons should be counted as different if they have different set of edges, even if they enclose the same area. For example, the polygon with vertices [(0,0),(0,3),(1,1),(3,0)] is distinct from the polygon with vertices [(0,0),(0,3),(1,1),(3,0),(1,0)].
For example, P(1) = 131, P(2) = 1648531, P(3) = 1099461296175 and P(343) mod 1&nbsp;000&nbsp;000&nbsp;007 = 937293740.
Find P(7^13) mod 1&nbsp;000&nbsp;000&nbsp;007.


## 解决方案


## 代码


