---
title: Project Euler 363
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 363
## 题目
### Bézier Curves

A cubic Bézier curve is defined by four points: $P_0, P_1, P_2,$ and $P_3$.

<div class="float_right"><img src="project/images/p363_bezier.png" class="dark_img" alt="p363_bezier.png" /></div>

The curve is constructed as follows:

On the segments $P_0 P_1$, $P_1 P_2$, and $P_2 P_3$ the points $Q_0, Q_1,$ and $Q_2$ are drawn such that $\dfrac{P_0 Q_0}{P_0 P_1} = \dfrac{P_1 Q_1}{P_1 P_2} = \dfrac{P_2 Q_2}{P_2 P_3} = t$, with $t$ in $[0, 1]$.

On the segments $Q_0 Q_1$ and $Q_1 Q_2$ the points $R_0$ and $R_1$ are drawn such that<br />
$\dfrac{Q_0 R_0}{Q_0 Q_1} = \dfrac{Q_1 R_1}{Q_1 Q_2} = t$ for the same value of $t$.

On the segment $R_0 R_1$ the point $B$ is drawn such that $\dfrac{R_0 B}{R_0 R_1} = t$ for the same value of $t$.

The Bézier curve defined by the points $P_0, P_1, P_2, P_3$ is the locus of $B$ as $Q_0$ takes all possible positions on the segment $P_0 P_1$.<br />
(Please note that for all points the value of $t$ is the same.)



From the construction it is clear that the Bézier curve will be tangent to the segments $P_0 P_1$ in $P_0$ and $P_2 P_3$ in $P_3$.

A cubic Bézier curve with $P_0 = (1, 0), P_1 = (1, v), P_2 = (v, 1),$ and $P_3 = (0, 1)$ is used to approximate a quarter circle.<br />
The value $v \gt 0$ is chosen such that the area enclosed by the lines $O P_0, OP_3$ and the curve is equal to $\dfrac{\pi}{4}$ (the area of the quarter circle).

By how many percent does the length of the curve differ from the length of the quarter circle?<br />
That is, if $L$ is the length of the curve, calculate $100 \times \dfrac{L - \frac{\pi}{2}}{\frac{\pi}{2}}$<br />
Give your answer rounded to 10 digits behind the decimal point.


# Project Euler 363
## 题目
### Bézier Curves

A cubic Bézier curve is defined by four points: P_0, P_1, P_2 and P_3.
<center><img src="https://projecteuler.net/project/images/p363_bezier.png"></center>

The curve is constructed as follows:<br>On the segments P_0P_1, P_1P_2 and P_2P_3 the points Q_0,Q_1 and Q_2 are drawn such that<br>P_0Q_0 / P_0P_1 = P_1Q_1 / P_1P_2 = P_2Q_2 / P_2P_3 = t (t in [0,1]).<br>On the segments Q_0Q_1 and Q_1Q_2 the points R_0 and R_1 are drawn such that<br>Q_0R_0  / Q_0Q_1 = Q_1R_1 / Q_1Q_2 = t for the same value of t.<br>On the segment R_0R_1 the point B is drawn such that R_0B / R_0R_1 = t for the same value of t.<br>The Bézier curve defined by the points P_0, P_1, P_2, P_3 is the locus of B as Q_0 takes all possible positions on the segment P_0P_1.<br>(Please note that for all points the value of t is the same.)
At <a href="http://home.kpn.nl/hklein/bezier/bezier.html" target="_blank">this (external) web address</a> you will find an applet that allows you to drag the points P_0, P_1, P_2 and P_3 to see what the Bézier curve (green curve) defined by those points looks like. You can also drag the point Q_0 along the segment P_0P_1.
From the construction it is clear that the Bézier curve will be tangent to the segments P_0P_1 in P_0 and P_2P_3 in P_3.
A cubic Bézier curve with P_0=(1,0), P_1=(1,v), P_2=(v,1) and P_3=(0,1) is used to approximate a quarter circle.<br>The value v > 0 is chosen such that the area enclosed by the lines OP_0, OP_3 and the curve is equal to ^π/_4 (the area of the quarter circle).
By how many percent does the length of the curve differ from the length of the quarter circle?
That is, if L is the length of the curve, calculate 100 \times $\frac{L − π/2}{π/2}$.
Give your answer rounded to 10 digits behind the decimal point.


## 解决方案


## 代码


