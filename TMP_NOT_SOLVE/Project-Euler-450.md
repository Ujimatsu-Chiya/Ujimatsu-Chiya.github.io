---
title: Project Euler 450
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 450
## 题目
### Hypocycloid and Lattice points

A hypocycloid is the curve drawn by a point on a small circle rolling inside a larger circle. The parametric equations of a hypocycloid centered at the origin, and starting at the right most point is given by:

$$x(t) = (R - r) \cos(t) + r \cos(\frac {R - r} r t)$$
$$y(t) = (R - r) \sin(t) - r \sin(\frac {R - r} r t)$$

Where $R$ is the radius of the large circle and $r$ the radius of the small circle.

Let $C(R, r)$ be the set of distinct points with integer coordinates on the hypocycloid with radius <var>R</var> and <var>r</var> and for which there is a corresponding value of <var>t</var> such that $\sin(t)$ and $\cos(t)$ are rational numbers.

Let $S(R, r) = \sum_{(x,y) \in C(R, r)} |x| + |y|$ be the sum of the absolute values of the $x$ and $y$ coordinates of the points in $C(R, r)$.

Let $T(N) = \sum_{R = 3}^N \sum_{r=1}^{\lfloor \frac {R - 1} 2 \rfloor} S(R, r)$ be the sum of $S(R, r)$ for <var>R</var> and <var>r</var> positive integers, $R\leq N$  and $2r < R$.

You are given:
<table><tr><td class="right">$C(3, 1)$</td><td>=</td><td>$\{(3, 0), (-1, 2), (-1,0), (-1,-2)\}$</td>
</tr><tr><td>$C(2500, 1000)$</td><td>=</td><td>$\{(2500, 0), (772, 2376), (772, -2376), (516, 1792), (516, -1792), (500, 0), (68, 504), (68, -504),$</td>
</tr><tr><td colspan="2"> </td><td>$(-1356, 1088), (-1356, -1088), (-1500, 1000), (-1500, -1000)\}$</td>
</tr></table><i>Note:</i> $(-625, 0)$ is not an element of $C(2500, 1000)$ because $\sin(t)$ is not a rational number for the corresponding values of $t$.

$S(3, 1) = (|3| + |0|) + (|-1| + |2|) + (|-1| + |0|) + (|-1| + |-2|) = 10$

$T(3) = 10; T(10) = 524; T(100) = 580442; T(10^3) = 583108600$.

Find $T(10^6)$.


# Project Euler 450
## 题目
### Hypocycloid and Lattice points

A hypocycloid is the curve drawn by a point on a small circle rolling inside a larger circle. The parametric equations of a hypocycloid centered at the origin, and starting at the right most point is given by:
$$x(t)=(R-r)\cos(t)+r \cos(\frac{R-r}{r}t)$$ $$y(t)=(R-r)\sin(t)-r \sin(\frac{R-r}{r}t)$$
Where R is the radius of the large circle and r the radius of the small circle.
Let $C(R,r)$ be the set of distinct points with integer coordinates on the hypocycloid with radius R and r and for which there is a corresponding value of t such that $\sin(t)$ and $\cos(t)$ are rational numbers.
Let $S(R,r)=\sum_{(x,y) \in C(R,r)}|x|+|y|$ be the sum of the absolute values of the x and y coordinates of the points in $C(R,r)$.
Let $T(N)=\sum_{R=3}^{N} \sum_{r=1}^{\lfloor \frac{R-1}{2} \rfloor}S(R,r)$ be the sum of $S(R,r)$ for R and r positive integers, $R \le N$ and $2r \lt R$.
You are given:<br>C(3, 1) = {(3, 0), (-1, 2), (-1,0), (-1,-2)}
C(2500, 1000) =
{(2500, 0), (772, 2376), (772, -2376), (516, 1792),(516, -1792), (500, 0), (68, 504), (68, -504),(-1356, 1088), (-1356, -1088), (-1500, 1000), (-1500, -1000)}
<em>Note: (-625, 0) is not an element of C(2500, 1000) because $\sin(t)$ is not a rational number for the corresponding values of t.</em>
S(3, 1) = (|3| + |0|) + (|-1| + |2|) + (|-1| + |0|) + (|-1| + |-2|) = 10
T(3) = 10; T(10) = 524; T(100) = 580442; T(10^3) = 583108600.
Find T(10^6).


## 解决方案


## 代码


