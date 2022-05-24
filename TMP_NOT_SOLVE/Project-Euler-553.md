---
title: Project Euler 553
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 553
## 题目
### Power sets of power sets

Let <var>P</var>(<var>n</var>) be the set of the first <var>n</var> positive integers {1, 2, \dots, <var>n</var>}.<br />
Let Q(<var>n</var>) be the set of all the non-empty subsets of <var>P</var>(<var>n</var>).<br />
Let R(<var>n</var>) be the set of all the non-empty subsets of <var>Q</var>(<var>n</var>).

An element <var>X</var> ∈ <var>R</var>(<var>n</var>) is a non-empty subset of <var>Q</var>(<var>n</var>), so it is itself a set.<br />
From <var>X</var> we can construct a graph as follows:

<ul><li>Each element <var>Y</var> ∈ <var>X</var> corresponds to a vertex and labeled with <var>Y</var>;</li>
<li>Two vertices <var>Y</var>_1 and <var>Y</var>_2 are connected if <var>Y</var>_1 ∩ <var>Y</var>_2 ≠ ∅.</li>
</ul>For example, <var>X</var> = {{1}, {1,2,3}, {3}, {5,6}, {6,7}} results in the following graph:

<div align="center"><img src="project/images/p553-power-sets.gif" alt="p553-power-sets.gif" /></div>

This graph has two <b>connected components</b>.

Let <var>C</var>(<var>n</var>,<var>k</var>) be the number of elements of <var>R</var>(<var>n</var>) that have exactly <var>k</var> connected components in their graph.<br />
You are given <var>C</var>(2,1) = 6, <var>C</var>(3,1) = 111, <var>C</var>(4,2) = 486, <var>C</var>(100,10) mod 1 000 000 007 = 728209718.

Find <var>C</var>(10^4,10) mod 1 000 000 007.


# Project Euler 553
## 题目
### Power sets of power sets

Let P(n) be the set of the first n positive integers {1, 2, \dots, n}.<br>Let Q(n) be the set of all the non-empty subsets of P(n).<br>Let R(n) be the set of all the non-empty subsets of Q(n).
An element X $\in$ R(n) is a non-empty subset of Q(n), so it is itself a set.<br>From X we can construct a graph as follows:
<ul>
<li>Each element Y $\in$ X corresponds to a vertex and labeled with Y;</li>
<li>Two vertices Y_1 and Y_2 are connected if Y_1$\cap$Y_2$\neq \emptyset$.</li>
</ul>
For example, X={ {1},{1,2,3},{3},{5,6},{6,7} } results in the following graph:
<center><img src="https://projecteuler.net/project/images/p553-power-sets.gif" alt="p553-power-sets.gif"></center>

This graph has two <b>connected components</b>.
Let C(n,k) be the number of elements of R(n) that have exactly k connected components in their graph.<br>You are given C(2,1)=6, C(3,1)=111, C(4,2)=486, C(100,10) mod 1000000007 = 728209718.
Find C(10^4,10) mod 1000000007.


## 解决方案


## 代码


