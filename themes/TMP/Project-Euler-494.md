---
title: Project Euler 494
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 494
## 题目
### Collatz prefix families


The Collatz sequence is defined as:
$a_{i+1} = \left\{  \large{\frac {a_i} 2 \atop 3 a_i+1} {\text{if }a_i\text{ is even} \atop \text{if }a_i\text{ is odd}} \right.$.


The Collatz conjecture states that starting from any positive integer, the sequence eventually reaches the cycle 1,4,2,1\dots.<br />
We shall define the sequence prefix <var>p(n)</var> for the Collatz sequence starting with <var>a_1 = n</var> as the sub-sequence of all numbers not a power of 2 (2^0=1 is considered a power of 2 for this problem). For example:<br /><var>p</var>(13) = {13, 40, 20, 10, 5} <br /><var>p</var>(8) = {}<br />
Any number invalidating the conjecture would have an infinite length sequence prefix.


Let <var>S_m</var> be the set of all sequence prefixes of length <var>m</var>. Two sequences {a_1, a_2, \dots, a_<var>m</var>} and {b_1, b_2, \dots, b_<var>m</var>} in <var>S_m</var> are said to belong to the same prefix family if a_i < a_j if and only if b_i < b_j for all 1 \le i,j \le<var> m</var>.


For example, in <var>S</var>_4, {6, 3, 10, 5} is in the same family as {454, 227, 682, 341}, but not {113, 340, 170, 85}.<br />
Let <var>f(m)</var> be the number of distinct prefix families in <var>S_m</var>.<br />
You are given <var>f</var>(5) = 5, <var>f</var>(10) = 55, <var>f</var>(20) = 6771.


Find f(90).




# Project Euler 494
## 题目
### Collatz prefix families

The Collatz sequence is defined as: 
$$a_{i+1} = \frac{a_i}{2} \text{ if }a_i\text{ is even}$$ $$a_{i+1} = 3a_i+1\text{ if }a_i\text{ is odd}$$
The Collatz conjecture states that starting from any positive integer, the sequence eventually reaches the cycle 1,4,2,1\dots.<br>We shall define the sequence prefix p(n) for the Collatz sequence starting with a_1 = n as the sub-sequence of all numbers not a power of 2 (2^0=1 is considered a power of 2 for this problem). For example:<br>p(13) = {13, 40, 20, 10, 5}<br>p(8) = {}<br>Any number invalidating the conjecture would have an infinite length sequence prefix.
Let S_m be the set of all sequence prefixes of length m. Two sequences {a_1, a_2, \dots, a_m} and {b_1, b_2, \dots, b_m} in S_m are said to belong to the same prefix family if a_i < a_j if and only if b_i < b_j for all 1 \le i,j \le m.
For example, in S_4, {6, 3, 10, 5} is in the same family as {454, 227, 682, 341}, but not {113, 340, 170, 85}.<br>Let f(m) be the number of distinct prefix families in S_m.<br>You are given f(5) = 5, f(10) = 55, f(20) = 6771.
Find f(90).


## 解决方案


## 代码


