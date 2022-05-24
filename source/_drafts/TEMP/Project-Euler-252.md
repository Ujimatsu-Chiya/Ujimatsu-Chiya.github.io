---
title: Project Euler 252
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 252
## 题目
### Convex Holes


Given a set of points on a plane, we define a convex hole to be a convex polygon having as vertices any of the given points and not containing any of the given points in its interior (in addition to the vertices, other given points may lie on the perimeter of the polygon). 


As an example, the image below shows a set of twenty points and a few such convex holes. 
The convex hole shown as a red heptagon has an area equal to 1049694.5 square units, which is the highest possible area for a convex hole on the given set of points.

<div class="center">
<img src="project/images/p252_convexhole.gif" class="dark_img" alt="" /></div>

For our example, we used the first 20 points (<var>T</var>_2<var>k</var>−1, <var>T</var>_2<var>k</var>), for <var>k</var> = 1,2,\dots,20, produced with the pseudo-random number generator:

<center><table class="p252"><tr><td style="text-align:right;"><var>S</var>_0</td>
    <td>=_ </td>
    <td>290797_ </td>
  </tr><tr><td><var>S</var>_<var>n</var>+1</td>
    <td>=_ </td>
    <td><var>S</var>_<var>n</var>^2 mod 50515093</td>
  </tr><tr><td style="text-align:right;"><var>T</var>_<var>n</var></td>
    <td>=_ </td>
    <td>( <var>S</var>_<var>n</var> mod 2000 ) − 1000^ </td>
  </tr></table></center>


<i>i.e.</i> (527, 144), (−488, 732), (−454, −947), \dots


What is the maximum area for a convex hole on the set containing the first 500 points in the pseudo-random sequence?<br /> Specify your answer including one digit after the decimal point.








# Project Euler 252
## 题目
### Convex Holes

Given a set of points on a plane, we define a convex hole to be a convex polygon having as vertices any of the given points and not containing any of the given points in its interior (in addition to the vertices, other given points may lie on the perimeter of the polygon). 
As an example, the image below shows a set of twenty points and a few such convex holes. The convex hole shown as a red heptagon has an area equal to 1049694.5 square units, which is the highest possible area for a convex hole on the given set of points.
<center><img src="https://projecteuler.net/project/images/p252_convexhole.gif" alt=""></center>

For our example, we used the first 20 points (T_2k−1,&thinsp;T_2k), for k&thinsp;=&thinsp;1,2,\dots,20, produced with the pseudo-random number generator:
<center>$S\_0=290797$
$S\_{n+1}=S\_n^2 \text{ mod } 50515093$
$T\_n=\text{(}S\_n \text{ mod } 2000 \text{)}-1000$
</center>

<em>i.e.</em> (527,&thinsp;144), (−488,&thinsp;732), (−454,&thinsp;−947), \dots
What is the maximum area for a convex hole on the set containing the first 500 points in the pseudo-random sequence?<br>Specify your answer including one digit after the decimal point.


## 解决方案


## 代码


