---
title: Project Euler 385
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 385
## 题目
### Ellipses inside triangles



For any triangle <var>T</var> in the plane, it can be shown that there is a unique ellipse with largest area that is completely inside <var>T</var>.
<p align="center">
<img src="project/images/p385_ellipsetriangle.png" alt="p385_ellipsetriangle.png" />

For a given <var>n</var>, consider triangles <var>T</var> such that:<br />
- the vertices of <var>T</var> have integer coordinates with absolute value \le n, and <br />
- the <b>foci</b>^1 of the largest-area ellipse inside <var>T</var> are (√13,0) and (-√13,0).<br />
Let A(<var>n</var>) be the sum of the areas of all such triangles.


For example, if <var>n</var> = 8, there are two such triangles. Their vertices are (-4,-3),(-4,3),(8,0) and (4,3),(4,-3),(-8,0), and the area of each triangle is 36. Thus A(8) = 36 + 36 = 72.


It can be verified that A(10) = 252, A(100) = 34632 and A(1000) = 3529008.


Find A(1 000 000 000).



<span style="font-size:smaller;">^1The <b>foci</b> (plural of <b>focus</b>) of an ellipse are two points A and B such that for every point P on the boundary of the ellipse, <var>AP</var> + <var>PB</var> is constant.</span>








# Project Euler 385
## 题目
### Ellipses inside triangles

For any triangle T in the plane, it can be shown that there is a unique ellipse with largest area that is completely inside T.
<center><img src="https://projecteuler.net/project/images/p385_ellipsetriangle.png"></center>

For a given n, consider triangles T such that:
<ul>
<li>the vertices of T have integer coordinates with absolute value \le n, and </li>
<li>the <b>foci</b>^1 of the largest-area ellipse inside T are (√13,0) and (-√13,0).<br>Let A(n) be the sum of the areas of all such triangles.</li>
</ul>
For example, if n = 8, there are two such triangles. Their vertices are (-4,-3),(-4,3),(8,0) and (4,3),(4,-3),(-8,0), and the area of each triangle is 36. Thus A(8) = 36 + 36 = 72.
It can be verified that A(10) = 252, A(100) = 34632 and A(1000) = 3529008.
Find A(1 000 000 000).
^1The <b>foci</b> (plural of <b>focus</b>) of an ellipse are two points A and B such that for every point P on the boundary of the ellipse, AP + PB is constant.


## 解决方案


## 代码


