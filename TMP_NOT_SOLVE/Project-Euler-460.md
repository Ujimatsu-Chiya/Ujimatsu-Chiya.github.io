---
title: Project Euler 460
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 460
## 题目
### An ant on the move


On the Euclidean plane, an ant travels from point A(0, 1) to point B(<var>d</var>, 1) for an integer <var>d</var>.


In each step, the ant at point (<var>x</var>_0, <var>y</var>_0) chooses one of the lattice points (<var>x</var>_1, <var>y</var>_1) which satisfy <var>x</var>_1 \ge 0 and <var>y</var>_1 \ge 1 and goes straight to (<var>x</var>_1, <var>y</var>_1) at a constant velocity <var>v</var>. The value of <var>v</var> depends on <var>y</var>_0 and <var>y</var>_1 as follows:
<ul><li> If <var>y</var>_0 = <var>y</var>_1, the value of <var>v</var> equals <var>y</var>_0.</li>
<li> If <var>y</var>_0 ≠ <var>y</var>_1, the value of <var>v</var> equals (<var>y</var>_1 - <var>y</var>_0) / (ln(<var>y</var>_1) - ln(<var>y</var>_0)).</li>
</ul>
The left image is one of the possible paths for <var>d</var> = 4. First the ant goes from A(0, 1) to P_1(1, 3) at velocity (3 - 1) / (ln(3) - ln(1)) ≈ 1.8205. Then the required time is sqrt(5) / 1.8205 ≈ 1.2283.<br />
From P_1(1, 3) to P_2(3, 3) the ant travels at velocity 3 so the required time is 2 / 3 ≈ 0.6667. From P_2(3, 3) to B(4, 1) the ant travels at velocity (1 - 3) / (ln(1) - ln(3)) ≈ 1.8205 so the required time is sqrt(5) / 1.8205 ≈ 1.2283.<br />
Thus the total required time is 1.2283 + 0.6667 + 1.2283 = 3.1233.


The right image is another path. The total required time is calculated as 0.98026 + 1 + 0.98026 = 2.96052. It can be shown that this is the quickest path for <var>d</var> = 4.

<p align="center"><img src="project/images/p460_ant.jpg" alt="p460_ant.jpg" />

Let F(<var>d</var>) be the total required time if the ant chooses the quickest path. For example, F(4) ≈ 2.960516287.<br />
We can verify that F(10) ≈ 4.668187834 and F(100) ≈ 9.217221972.


Find F(10000). Give your answer rounded to nine decimal places.



# Project Euler 460
## 题目
### An ant on the move

On the Euclidean plane, an ant travels from point A(0, 1) to point B(d, 1) for an integer d.
In each step, the ant at point (x_0, y_0) chooses one of the lattice points (x_1, y_1) which satisfy x_1 \ge 0 and y_1 \ge 1 and goes straight to (x_1, y_1) at a constant velocity v. The value of v depends on y_0 and y_1 as follows:
<ul>
<li>If y_0 = y_1, the value of v equals y_0.</li>
<li>If y_0 ≠ y_1, the value of v equals (y_1 - y_0) / (ln(y_1) - ln(y_0)).</li>
</ul>
The left image is one of the possible paths for d = 4. First the ant goes from A(0, 1) to P_1(1, 3) at velocity (3 - 1) / (ln(3) - ln(1)) ≈ 1.8205. Then the required time is sqrt(5) / 1.8205 ≈ 1.2283.<br>From P_1(1, 3) to P_2(3, 3) the ant travels at velocity 3 so the required time is 2 / 3 ≈ 0.6667. From P_2(3, 3) to B(4, 1) the ant travels at velocity (1 - 3) / (ln(1) - ln(3)) ≈ 1.8205 so the required time is sqrt(5) / 1.8205 ≈ 1.2283.<br>Thus the total required time is 1.2283 + 0.6667 + 1.2283 = 3.1233.
The right image is another path. The total required time is calculated as 0.98026 + 1 + 0.98026 = 2.96052. It can be shown that this is the quickest path for d = 4.
<center><img src="https://projecteuler.net/project/images/p460_ant.jpg"></center>

Let F(d) be the total required time if the ant chooses the quickest path. For example, F(4) ≈ 2.960516287.<br>We can verify that F(10) ≈ 4.668187834 and F(100) ≈ 9.217221972.
Find F(10000). Give your answer rounded to nine decimal places.


## 解决方案


## 代码


