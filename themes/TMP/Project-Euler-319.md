---
title: Project Euler 319
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 319
## 题目
### Bounded Sequences


Let <var>x</var>_1, <var>x</var>_2,\dots, <var>x_n</var> be a sequence of length <var>n</var> such that:
<ul><li><var>x</var>_1 = 2</li>
<li>for all 1 < <var>i</var> \le <var>n</var> : <var>x</var>_<var>i</var>-<i>1</i> < <var>x_i</var></li>
<li>for all <var>i</var> and <var>j</var> with 1 \le <var>i</var>, <var>j</var> \le <var>n</var> : (<var>x_i</var>)<var>^ j</var> < (<var>x_j</var> + 1)<var>^i</var></li>
</ul>
There are only five such sequences of length 2, namely:
{2,4}, {2,5}, {2,6}, {2,7} and {2,8}.<br />
There are 293 such sequences of length 5; three examples are given below:<br />
{2,5,11,25,55}, {2,6,14,36,88}, {2,8,22,64,181}.


Let <var>t</var>(<var>n</var>) denote the number of such sequences of length <var>n</var>.<br />
You are given that <var>t</var>(10) = 86195 and <var>t</var>(20) = 5227991891.


Find <var>t</var>(10^10) and give your answer modulo 10^9.





# Project Euler 319
## 题目
### Bounded Sequences

Let x_1, x_2,\dots, x_n be a sequence of length n such that:
<ul>
<li>x_1 = 2</li>
<li>for all 1 < i \le n : x_i-<i>1</i> < x_i</li>
<li>for all i and j with 1 \le i, j \le n : (x_i)^j < (x_j + 1)^i</li>
</ul>
There are only five such sequences of length 2, namely: {2,4}, {2,5}, {2,6}, {2,7} and {2,8}.<br>There are 293 such sequences of length 5; three examples are given below:<br>{2,5,11,25,55}, {2,6,14,36,88}, {2,8,22,64,181}.
Let t(n) denote the number of such sequences of length n.<br>You are given that t(10) = 86195 and t(20) = 5227991891.
Find t(10^10) and give your answer modulo 10^9.


## 解决方案


## 代码


