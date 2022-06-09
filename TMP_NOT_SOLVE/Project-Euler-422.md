---
title: Project Euler 422
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 422
## 题目
### Sequence of points on a hyperbola

Let H be the hyperbola defined by the equation 12<var>x</var>^2 + 7<var>x</var><var>y</var> - 12<var>y</var>^2 = 625.

Next, define X as the point (7, 1). It can be seen that X is in H.

Now we define a sequence of points in H, {P_<var>i</var> : <var>i</var> \ge 1}, as:
<ul><li> P_1 = (13, 61/4).
</li><li> P_2 = (-43/6, -4).
</li><li> For <var>i</var> > 2, P_<var>i</var> is the unique point in H that is different from P_<var>i</var>-1 and such that line P_<var>i</var>P_<var>i</var>-1 is parallel to line P_<var>i</var>-2X. It can be shown that P_<var>i</var> is well-defined, and that its coordinates are always rational.
</li></ul><div class="center"><img src="project/images/p422_hyperbola.gif" class="dark_img" alt="p422_hyperbola.gif" /></div>
You are given that P_3  = (-19/2, -229/24), P_4 = (1267/144, -37/12) and P_7 = (17194218091/143327232, 274748766781/1719926784).

Find P_<var>n</var> for <var>n</var> = 11^14 in the following format:<br />If P_<var>n</var> = (<var>a</var>/<var>b</var>, <var>c</var>/<var>d</var>) where the fractions are in lowest terms and the denominators are positive, then the answer is (<var>a</var> + <var>b</var> + <var>c</var> + <var>d</var>) mod 1 000 000 007.

For <var>n</var> = 7, the answer would have been: 806236837.


# Project Euler 422
## 题目
### Sequence of points on a hyperbola

Let H be the hyperbola defined by the equation 12x^2 + 7xy - 12y^2 = 625.
Next, define X as the point (7, 1). It can be seen that X is in H.<br>Now we define a sequence of points in H, {P_i : i \ge 1}, as:
<ul>
<li>P_1 = (13, 61/4).</li>
<li>P_2 = (-43/6, -4).</li>
<li>For i > 2, P_i is the unique point in H that is different from P_i-1 and such that line P_iP_i-1 is parallel to line P_i-2X. It can be shown that P_i is well-defined, and that its coordinates are always rational.</li>
</ul>
<img src="https://projecteuler.net/project/images/p422_hyperbola.gif">

You are given that P_3  = (-19/2, -229/24), P_4 = (1267/144, -37/12) and P_7 = (17194218091/143327232, 274748766781/1719926784).
Find P_n for n = 11^14 in the following format:<br>If P_n = (a/b, c/d) where the fractions are in lowest terms and the denominators are positive, then the answer is (a + b + c + d) mod 1&nbsp;000&nbsp;000&nbsp;007.
For n = 7, the answer would have been: 806236837.


## 解决方案


## 代码


