---
title: Project Euler 537
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 537
## 题目
### Counting tuples


Let <var>π</var>(<var>x</var>) be the prime counting function, i.e. the number of prime numbers less than or equal to <var>x</var>.<br />
For example, <var>π</var>(1)=0, <var>π</var>(2)=1, <var>π</var>(100)=25.


Let <var>T</var>(<var>n</var>,<var>k</var>) be the number of <var>k</var>-tuples (<var>x</var>_1,\dots,<var>x_k</var>) which satisfy:<br />
1. every <var>x_i</var> is a positive integer;<br />
2. $\displaystyle \sum_{i=1}^k \pi(x_i)=n$


For example <var>T</var>(3,3)=19.<br />
The 19 tuples are (1,1,5), (1,5,1), (5,1,1), (1,1,6), (1,6,1), (6,1,1), (1,2,3), (1,3,2), (2,1,3), (2,3,1), (3,1,2), (3,2,1), (1,2,4), (1,4,2), (2,1,4), (2,4,1), (4,1,2), (4,2,1), (2,2,2).


You are given <var>T</var>(10,10) = 869 985 and <var>T</var>(10^3,10^3) ≡ 578 270 566 (mod 1 004 535 809).

Find <var>T</var>(20 000, 20 000) mod 1 004 535 809.






# Project Euler 537
## 题目
### Counting tuples

Let π(x) be the prime counting function, i.e. the number of prime numbers less than or equal to x.<br>For example, π(1)=0, π(2)=1, π(100)=25.
Let T(n,k) be the number of k-tuples (x_1,\dots,x_k) which satisfy:
<ol>
<li>every x_i is a positive integer;</li>
<li>$\displaystyle \sum_{i=1}^k \pi(x_i)=n$</li>
</ol>
For example T(3,3)=19.<br>The 19 tuples are (1,1,5), (1,5,1), (5,1,1), (1,1,6), (1,6,1), (6,1,1), (1,2,3), (1,3,2), (2,1,3), (2,3,1), (3,1,2), (3,2,1), (1,2,4), (1,4,2), (2,1,4), (2,4,1), (4,1,2), (4,2,1), (2,2,2).
You are given T(10,10) = 869 985 and T(10^3,10^3) ≡ 578 270 566 (mod 1 004 535 809).
Find T(20 000, 20 000) mod 1 004 535 809.


## 解决方案


## 代码


