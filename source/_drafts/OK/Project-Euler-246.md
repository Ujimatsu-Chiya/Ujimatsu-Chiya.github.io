---
title: Project Euler 246
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 246
## 题目
### Tangents to an ellipse

A definition for an ellipse is:

Given a circle $c$ with centre $M$ and radius $r$ and a point $G$ such that $d(G,M)<r$, the locus of the points that are equidistant from $c$ and $G$ form an ellipse.

The construction of the points of the ellipse is shown below.

![](../images/p246_anim.gif)

Given are the points $M(-2000,1500)$ and $G(8000,1500)$. 

Given is also the circle $c$ with centre $M$ and radius $15000$.

The locus of the points that are equidistant from $G$ and $c$ form an ellipse $e$.

From a point $P$ outside $e$ the two tangents $t_1$ and $t_2$ to the ellipse are drawn.

Let the points where $t_1$ and $t_2$ touch the ellipse be $R$ and $S$.

![](../images/p246_ellipse.gif)

For how many lattice points $P$ is angle $RPS$ greater than $45$ degrees?


## 解决方案

$|EG|=|EU|$，$|EU|+|EM|=r$，因此$|EG|+|EM|=r=2a$，其中$2a$是椭圆的长轴长度，焦距$2c=d(G,M)$。由于椭圆的中心也在个点，那么为了方便处理问题，将椭圆的中心挪到原点，那么可以写成椭圆的标准方程：

$$\dfrac{x^2}{a^2}+\dfrac{y^2}{b^2}=1$$

其中$a=7500,c=5000,b=a^2-c^2$。

那么，由于椭圆关于两个坐标轴对称，因此只考虑第一象限以及$x,y$轴正半轴上的格点。


## 代码


