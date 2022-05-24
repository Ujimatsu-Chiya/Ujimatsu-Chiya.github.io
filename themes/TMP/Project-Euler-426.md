---
title: Project Euler 426
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 426
## 题目
### Box-ball system


Consider an infinite row of boxes. Some of the boxes contain a ball. For example, an initial configuration of 2 consecutive occupied boxes followed by 2 empty boxes, 2 occupied boxes, 1 empty box, and 2 occupied boxes can be denoted by the sequence (2, 2, 2, 1, 2), in which the number of consecutive occupied and empty boxes appear alternately.


A turn consists of moving each ball exactly once according to the following rule: Transfer the leftmost ball which has not been moved to the nearest empty box to its right.


After one turn the sequence (2, 2, 2, 1, 2) becomes (2, 2, 1, 2, 3) as can be seen below; note that we begin the new sequence starting at the first occupied box.


<div align="center">
<img src="project/images/p426_baxball1.gif" alt="p426_baxball1.gif" /></div>


A system like this is called a <b>Box-Ball System</b> or <b>BBS</b> for short.


It can be shown that after a sufficient number of turns, the system evolves to a state where the consecutive numbers of occupied boxes is invariant. In the example below, the consecutive numbers of <b>occupied boxes</b> evolves to [1, 2, 3]; we shall call this the final state.


<div align="center">
<img src="project/images/p426_baxball2.gif" alt="p426_baxball2.gif" /></div>


We define the sequence {<var>t</var>_<var>i</var>}:<br /><ul><li><var>s</var>_0 = 290797
</li><li><var>s</var>_<var>k</var>+1 = <var>s</var>_<var>k</var>^2 mod 50515093
</li><li><var>t</var>_<var>k</var> = (<var>s</var>_<var>k</var> mod 64) + 1
</li></ul>
Starting from the initial configuration (<var>t</var>_0, <var>t</var>_1, \dots, <var>t</var>_10), the final state becomes [1, 3, 10, 24, 51, 75].<br />
Starting from the initial configuration (<var>t</var>_0, <var>t</var>_1, \dots, <var>t</var>_10 000 000), find the final state.<br />
Give as your answer the sum of the squares of the elements of the final state. For example, if the final state is [1, 2, 3] then 14 ( = 1^2 + 2^2 + 3^2) is your answer.



# Project Euler 426
## 题目
### Box-ball system

Consider an infinite row of boxes. Some of the boxes contain a ball. For example, an initial configuration of 2 consecutive occupied boxes followed by 2 empty boxes, 2 occupied boxes, 1 empty box, and 2 occupied boxes can be denoted by the sequence (2, 2, 2, 1, 2), in which the number of consecutive occupied and empty boxes appear alternately.
A turn consists of moving each ball exactly once according to the following rule: Transfer the leftmost ball which has not been moved to the nearest empty box to its right.
After one turn the sequence (2, 2, 2, 1, 2) becomes (2, 2, 1, 2, 3) as can be seen below; note that we begin the new sequence starting at the first occupied box.
<center><img src="https://projecteuler.net/project/images/p426_baxball1.gif"></center>

A system like this is called a **Box-Ball System** or **BBS** for short.
It can be shown that after a sufficient number of turns, the system evolves to a state where the consecutive numbers of occupied boxes is invariant. In the example below, the consecutive numbers of **occupied boxes** evolves to [1, 2, 3]; we shall call this the final state.
<center><img src="https://projecteuler.net/project/images/p426_baxball2.gif"></center>

We define the sequence {t_i}:
<ul>
<li>s_0 = 290797</li>
<li>s_k+1 = s_k^2 mod 50515093</li>
<li>t_k = (s_k mod 64) + 1</li>
</ul>
Starting from the initial configuration (t_0, t_1, \dots, t_10), the final state becomes [1, 3, 10, 24, 51, 75].<br>Starting from the initial configuration (t_0, t_1, \dots, t_10 000 000), find the final state.<br>Give as your answer the sum of the squares of the elements of the final state. For example, if the final state is [1, 2, 3] then 14 ( = 1^2 + 2^2 + 3^2) is your answer.


## 解决方案


## 代码


