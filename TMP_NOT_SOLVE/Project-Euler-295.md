---
title: Project Euler 295
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 295
## 题目
### Lenticular holes

We call the convex area enclosed by two circles a <i>lenticular hole</i> if:
<ul><li>The centres of both circles are on lattice points.</li>
<li>The two circles intersect at two distinct lattice points.</li>
<li>The interior of the convex area enclosed by both circles does not contain any lattice points.
</li>
</ul>Consider the circles:<br />
C_0: <var>x</var>^2+<var>y</var>^2=25<br />
C_1: (<var>x</var>+4)^2+(<var>y</var>-4)^2=1<br />
C_2: (<var>x</var>-12)^2+(<var>y</var>-4)^2=65


The circles C_0, C_1 and C_2 are drawn in the picture below.
<div align="center"><img src="project/images/p295_lenticular.gif" alt="p295_lenticular.gif" /></div>

C_0 and C_1 form a lenticular hole, as well as C_0 and C_2.

We call an ordered pair of positive real numbers (r_1, r_2) a <i>lenticular pair</i> if there exist two circles with radii r_1 and r_2 that form a lenticular hole.
We can verify that (1, 5) and (5, √65) are the lenticular pairs of the example above.

Let L(N) be the number of <b>distinct</b> lenticular pairs (r_1, r_2) for which 0 < r_1 \le r_2 \le N.<br />
We can verify that L(10) = 30 and L(100) = 3442.

Find L(100 000).















# Project Euler 295
## 题目
### Lenticular holes

Consider the circles:<br>C_0: x^2+y^2=25<br>C_1: (x+4)^2+(y-4)^2=1<br>C_2: (x-12)^2+(y-4)^2=65
The circles C_0, C_1 and C_2 are drawn in the picture below.
<center><img src="https://projecteuler.net/project/images/p295_lenticular.gif"></center>

C_0 and C_1 form a lenticular hole, as well as C_0 and C_2.
We call an ordered pair of positive real numbers (r_1, r_2) a <i>lenticular pair</i> if there exist two circles with radii r_1 and r_2 that form a lenticular hole. We can verify that (1, 5) and (5, √65) are the lenticular pairs of the example above.
Let L(N) be the number of <b>distinct</b> lenticular pairs (r_1, r_2) for which 0 < r_1 \le r_2 \le N.<br>We can verify that L(10) = 30 and L(100) = 3442.
Find L(100 000).


## 解决方案


## 代码


