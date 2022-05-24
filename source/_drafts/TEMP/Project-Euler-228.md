---
title: Project Euler 228
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 228
## 题目
### Minkowski Sums

Let <var>S</var>_n be the regular <var>n</var>-sided polygon – or <i>shape</i> – whose vertices 

<var>v</var>_<var>k</var> (<var>k</var> = 1,2,\dots,<var>n</var>) have coordinates:
<table><tr><td width="40"></td>
    <td><var>x</var>_<var>k</var>   =  
        cos( ^2<var>k</var>-1/_<var>n</var> \times180° )</td>
  </tr><tr><td width="40"></td>
    <td><var>y</var>_<var>k</var>   =  
        sin( ^2<var>k</var>-1/_<var>n</var> \times180° )</td>
  </tr></table>Each <var>S</var>_<var>n</var> is to be interpreted as a filled shape consisting of all points on the perimeter and in the interior.

The <i>Minkowski sum</i>, <var>S</var>+<var>T</var>, of two shapes <var>S</var> and <var>T</var> is the result of 

adding every point in <var>S</var> to every point in <var>T</var>, where point addition is performed coordinate-wise: 

(<var>u</var>, <var>v</var>) + (<var>x</var>, <var>y</var>) = (<var>u</var>+<var>x</var>, <var>v</var>+<var>y</var>).

For example, the sum of <var>S</var>_3 and <var>S</var>_4 is the six-sided shape shown in pink below:

<div class="center">
<img src="project/images/p228.png" class="dark_img" alt="picture showing S_3 + S_4" /></div>

How many sides does <var>S</var>_1864 + <var>S</var>_1865 + \dots + <var>S</var>_1909 have?


# Project Euler 228
## 题目
### Minkowski Sums

Let S_n be the regular n-sided polygon – or <i>shape</i> – whose vertices v_k (k&thinsp;=&thinsp;1,2,\dots,n) have coordinates:
<center>$x_k= \text{cos(}\frac{2k-1}{n} \times 180^\circ \text{)}$
$y_k= \text{sin(}\frac{2k-1}{n} \times 180^\circ \text{)}$
</center>

Each S_n is to be interpreted as a filled shape consisting of all points on the perimeter and in the interior.
The <i>Minkowski sum</i>, S+T, of two shapes S and T is the result of adding every point in S to every point in T, where point addition is performed coordinate-wise: (u,&thinsp;v) + (x,&thinsp;y) = (u+x,&thinsp;v+y).
For example, the sum of S_3 and S_4 is the six-sided shape shown in pink below:
<center><img src="https://projecteuler.net/project/images/p228.png" alt="picture showing S_3 + S_4"></center>

How many sides does S_1864&thinsp;+&thinsp;S_1865&thinsp;+&thinsp;\dots&thinsp;+&thinsp;S_1909 have?


## 解决方案


## 代码


