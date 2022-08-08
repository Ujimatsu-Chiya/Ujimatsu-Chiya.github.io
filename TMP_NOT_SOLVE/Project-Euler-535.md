---
title: Project Euler 535
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 535
## 题目
### Fractal Sequence


Consider the infinite integer sequence S starting with:<br /><var>S</var> = 1, 1, 2, 1, 3, 2, 4, 1, 5, 3, 6, 2, 7, 8, 4, 9, 1, 10, 11, 5, \dots

Circle the first occurrence of each integer.<br /><var>S</var> = ①, 1, ②, 1, ③, 2, ④, 1, ⑤, 3, ⑥, 2, ⑦, ⑧, 4, ⑨, 1, ⑩, ⑪, 5, \dots

The sequence is characterized by the following properties:
<ul><li>The circled numbers are consecutive integers starting with 1.</li>
<li>Immediately preceding each non-circled numbers <var>a_i</var>, there are exactly ⌊√<var>a_i</var>⌋ adjacent circled numbers, where ⌊⌋ is the floor function.</li>
<li>If we remove all circled numbers, the remaining numbers form a sequence identical to <var>S</var>, so <var>S</var> is a <b>fractal sequence</b>.</li></ul>Let T(<var>n</var>) be the sum of the first <var>n</var> elements of the sequence.<br />
You are given T(1) = 1, T(20) = 86, T(10^3) = 364089 and T(10^9) = 498676527978348241.

Find T(10^18). Give the last 9 digits of your answer.


# Project Euler 535
## 题目
### Fractal Sequence

Consider the infinite integer sequence S starting with:<br>S = 1, 1, 2, 1, 3, 2, 4, 1, 5, 3, 6, 2, 7, 8, 4, 9, 1, 10, 11, 5, \dots
Circle the first occurrence of each integer.<br>S = ①, 1, ②, 1, ③, 2, ④, 1, ⑤, 3, ⑥, 2, ⑦, ⑧, 4, ⑨, 1, ⑩, ⑪, 5, \dots
The sequence is characterized by the following properties:
<ul>
<li>The circled numbers are consecutive integers starting with 1.</li>
<li>Immediately preceding each non-circled numbers a_i, there are exactly ⌊√a_i⌋ adjacent circled numbers, where ⌊⌋ is the floor function.</li>
<li>If we remove all circled numbers, the remaining numbers form a sequence identical to S, so S is a <b>fractal sequence</b>.</li>
</ul>
Let T(n) be the sum of the first n elements of the sequence.<br>You are given T(1)&nbsp;=&nbsp;1, T(20)&nbsp;=&nbsp;86, T(10^3)&nbsp;=&nbsp;364089 and T(10^9)&nbsp;=&nbsp;498676527978348241.
Find T(10^18). Give the last 9 digits of your answer.


## 解决方案


## 代码


