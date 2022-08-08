---
title: Project Euler 382
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 382
## 题目
### Generating polygons



A <b>polygon</b> is a flat shape consisting of straight line segments that are joined to form a closed chain or circuit. A polygon consists of at least three sides and does not self-intersect.



A set S of positive numbers is said to <i>generate a polygon</i> P if:<ul><li> no two sides of P are the same length,
</li><li> the length of every side of P is in S, and
</li><li> S contains no other value.
</li></ul>
For example:<br />
The set {3, 4, 5} generates a polygon with sides 3, 4, and 5 (a triangle).<br />
The set {6, 9, 11, 24} generates a polygon with sides 6, 9, 11, and 24 (a quadrilateral).<br />
The sets {1, 2, 3} and {2, 3, 4, 9} do not generate any polygon at all.<br />


Consider the sequence s, defined as follows:<ul><li>s_1 = 1, s_2 = 2, s_3 = 3
</li><li>s_<var>n</var> = s_<var>n</var>-1 + s_<var>n</var>-3 for <var>n</var> > 3.
</li></ul>
Let U_<var>n</var> be the set {s_1, s_2, \dots, s_<var>n</var>}. For example, U_10 = {1, 2, 3, 4, 6, 9, 13, 19, 28, 41}.<br />
Let f(<var>n</var>) be the number of subsets of U_<var>n</var> which generate at least one polygon.<br />
For example, f(5) = 7, f(10) = 501 and f(25) = 18635853.



Find the last 9 digits of f(10^18).



# Project Euler 382
## 题目
### Generating polygons

A <b>polygon</b> is a flat shape consisting of straight line segments that are joined to form a closed chain or circuit. A polygon consists of at least three sides and does not self-intersect.
A set S of positive numbers is said to <i>generate a polygon</i> P if:
<ul>
<li>no two sides of P are the same length,</li>
<li>the length of every side of P is in S, and</li>
<li>S contains no other value.</li>
</ul>
For example:<br>The set {3, 4, 5} generates a polygon with sides 3, 4, and 5 (a triangle).<br>The set {6, 9, 11, 24} generates a polygon with sides 6, 9, 11, and 24 (a quadrilateral).<br>The sets {1, 2, 3} and {2, 3, 4, 9} do not generate any polygon at all.
Consider the sequence s, defined as follows:
<ul>
<li>s_1 = 1, s_2 = 2, s_3 = 3</li>
<li>s_n = s_n-1 + s_n-3 for n > 3.</li>
</ul>
Let U_n be the set {s_1, s_2, \dots, s_n}. For example, U_10 = {1, 2, 3, 4, 6, 9, 13, 19, 28, 41}.<br>Let f(n) be the number of subsets of U_n which generate at least one polygon.<br>For example, f(5) = 7, f(10) = 501 and f(25) = 18635853.
Find the last 9 digits of f(10^18).


## 解决方案


## 代码


