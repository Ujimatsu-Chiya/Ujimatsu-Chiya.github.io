---
title: Project Euler 316
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 316
## 题目
### Numbers in decimal expansions

Let <var>p</var> = <var>p_<font size="-2">1</font> p_<font size="-2">2</font> p_<font size="-2">3</font></var> \dots be an infinite sequence of random digits, selected from {0,1,2,3,4,5,6,7,8,9} with equal probability.<br />
It can be seen that <var>p</var> corresponds to the real number 0.<var>p_<font size="-2">1</font> p_<font size="-2">2</font> p_<font size="-2">3</font></var> \dots. <br />
It can also be seen that choosing a random real number from the interval [0,1) is equivalent to choosing an infinite sequence of random digits selected from {0,1,2,3,4,5,6,7,8,9} with equal probability.

For any positive integer <var>n</var> with <var>d</var> decimal digits, let <var>k</var> be the smallest index such that <br /><var>p_<small>k</small>, </var><var>p_<small>k+1</small></var>, \dots<var>p_<small>k+d-1</small></var> are the decimal digits of <var>n</var>, in the same order.<br />
Also, let <var>g</var>(<var>n</var>) be the expected value of <var>k</var>; it can be proven that <var>g</var>(<var>n</var>) is always finite and, interestingly, always an integer number.

For example, if <var>n</var> = 535, then<br />
for <var>p</var> = 31415926<b>535</b>897\dots., we get <var>k</var> = 9<br />
for <var>p</var> = 35528714365004956000049084876408468<b>535</b>4\dots, we get <var>k</var> = 36<br />
etc and we find that <var>g</var>(535) = 1008.

Given that $\sum \limits_{n = 2}^{999} {g \left ( \left \lfloor \dfrac{10^6}{n} \right \rfloor \right )} = 27280188$, find $\sum \limits_{n = 2}^{999999} {g \left ( \left \lfloor \dfrac{10^{16}}{n} \right \rfloor \right )}$.

<u><i>Note</i></u>: $\lfloor x \rfloor$ represents the floor function.


# Project Euler 316
## 题目
### Numbers in decimal expansions

Let p = p_1 p_2 p_3 \dots be an infinite sequence of random digits, selected from {0,1,2,3,4,5,6,7,8,9} with equal probability.<br>It can be seen that p corresponds to the real number 0.p_1 p_2 p_3 \dots.<br>It can also be seen that choosing a random real number from the interval [0,1) is equivalent to choosing an infinite sequence of random digits selected from {0,1,2,3,4,5,6,7,8,9} with equal probability.
For any positive integer n with d decimal digits, let k be the smallest index such that  p_k, p_k+1, \dotsp_k+d-1 are the decimal digits of n, in the same order.<br>Also, let g(n) be the expected value of k; it can be proven that g(n) is always finite and, interestingly, always an integer number.
For example, if n = 535, then<br>for p = 31415926**535**897\dots., we get k = 9<br>for p = 35528714365004956000049084876408468**535**4\dots, we get k = 36<br>etc and we find that g(535) = 1008.
Given that $\sum^{999}_{n=2}g(\lfloor \frac{10^6}{n} \rfloor)=27280188$, find $\sum^{999999}_{n=2}g(\lfloor \frac{10^{16}}{n} \rfloor)$。
<u><em>Note</em></u> : $\lfloor x \rfloor$ represents the floor function.


## 解决方案


## 代码


