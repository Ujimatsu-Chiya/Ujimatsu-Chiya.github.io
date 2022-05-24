---
title: Project Euler 428
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 428
## 题目
### Necklace of circles

Let <var>a</var>, <var>b</var> and <var>c</var> be positive numbers.<br />
Let W, X, Y, Z be four collinear points where |WX| = <var>a</var>, |XY| = <var>b</var>, |YZ| = <var>c</var> and |WZ| = <var>a</var> + <var>b</var> + <var>c</var>.<br />
Let C_in be the circle having the diameter XY.<br />
Let C_out be the circle having the diameter WZ.<br />


The triplet (<var>a</var>, <var>b</var>, <var>c</var>) is called a <em>necklace triplet</em> if you can place <var>k</var> \ge 3 distinct circles C_1, C_2, \dots, C_<var>k</var> such that:
<ul><li>C_<var>i</var> has no common interior points with any C_<var>j</var> for 1 \le <var>i</var>, <var>j</var> \le <var>k</var> and <var>i</var> ≠ <var>j</var>,
</li><li>C_<var>i</var> is tangent to both C_in and C_out for 1 \le <var>i</var> \le <var>k</var>,
</li><li>C_<var>i</var> is tangent to C_<var>i</var>+1 for 1 \le <var>i</var> < <var>k</var>, and
</li><li>C_<var>k</var> is tangent to C_1.
</li></ul>
For example, (5, 5, 5) and (4, 3, 21) are necklace triplets, while it can be shown that (2, 2, 5) is not.

<p align="center"><img src="project/images/p428_necklace.png" class="dark_img" alt="p428_necklace.png" />


Let T(<var>n</var>) be the number of necklace triplets (<var>a</var>, <var>b</var>, <var>c</var>) such that <var>a</var>, <var>b</var> and <var>c</var> are positive integers, and <var>b</var> \le <var>n</var>.
For example, T(1) = 9, T(20) = 732 and T(3000) = 438106.


Find T(1 000 000 000).



# Project Euler 428
## 题目
### Necklace of circles

Let a, b and c be positive numbers.<br>Let W, X, Y, Z be four collinear points where |WX| = a, |XY| = b, |YZ| = c and |WZ| = a + b + c.<br>Let C_in be the circle having the diameter XY.<br>Let C_out be the circle having the diameter WZ.
The triplet (a, b, c) is called a <em>necklace triplet</em> if you can place k \ge 3 distinct circles C_1, C_2, \dots, C_k such that:
<ul>
<li>C_i has no common interior points with any C_j for 1 \le i, j \le k and i ≠ j,</li>
<li>C_i is tangent to both C_in and C_out for 1 \le i \le k,</li>
<li>C_i is tangent to C_i+1 for 1 \le i < k, and</li>
<li>C_k is tangent to C_1.</li>
</ul>
For example, (5, 5, 5) and (4, 3, 21) are necklace triplets, while it can be shown that (2, 2, 5) is not.
<center><img src="https://projecteuler.net/project/images/p428_necklace.png"></center>

Let T(n) be the number of necklace triplets (a, b, c) such that a, b and c are positive integers, and b \le n. For example, T(1)&nbsp;=&nbsp;9, T(20)&nbsp;=&nbsp;732 and T(3000)&nbsp;=&nbsp;438106.
Find T(1&nbsp;000&nbsp;000&nbsp;000).


## 解决方案


## 代码


