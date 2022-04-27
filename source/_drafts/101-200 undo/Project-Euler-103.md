---
title: Project Euler 103
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 103
## 题目
### Special subset sums: optimum

Let S(A) represent the sum of elements in set A of size <i>n</i>. We shall call it a special sum set if for any two non-empty disjoint subsets, B and C, the following properties are true:
<ol><li>S(B) ≠ S(C); that is, sums of subsets cannot be equal.</li>
<li>If B contains more elements than C then S(B) &gt; S(C).</li>
</ol>If S(A) is minimised for a given <i>n</i>, we shall call it an optimum special sum set. The first five optimum special sum sets are given below.
<p class="margin_left"><i>n</i> = 1: {1}<br /><i>n</i> = 2: {1, 2}<br /><i>n</i> = 3: {2, 3, 4}<br /><i>n</i> = 4: {3, 5, 6, 7}<br /><i>n</i> = 5: {6, 9, 11, 12, 13}
It <i>seems</i> that for a given optimum set, A = {<i>a</i>_1, <i>a</i>_2, \dots , <i>a</i>_n}, the next optimum set is of the form B = {<i>b</i>, <i>a</i>_1+<i>b</i>, <i>a</i>_2+<i>b</i>, \dots ,<i>a</i>_n+<i>b</i>}, where <i>b</i> is the "middle" element on the previous row.
By applying this "rule" we would expect the optimum set for <i>n</i> = 6 to be A = {11, 17, 20, 22, 23, 24}, with S(A) = 117. However, this is not the optimum set, as we have merely applied an algorithm to provide a near optimum set. The optimum set for <i>n</i> = 6 is A = {11, 18, 19, 20, 22, 25}, with S(A) = 115 and corresponding set string: 111819202225.
Given that A is an optimum special sum set for <i>n</i> = 7, find its set string.
<p class="smaller">NOTE: This problem is related to <a href="problem=105">Problem 105</a> and <a href="problem=106">Problem 106</a>.


# Project Euler 103
## 题目
### Special subset sums: optimum
Let $S(A)$ represent the sum of elements in set $A$ of size $n$. We shall call it a special sum set if for any two non-empty disjoint subsets, $B$ and $C$, the following properties are true:
<ol>
<li>$S(B) \neq S(C)$; that is, sums of subsets cannot be equal.</li>
<li>If $B$ contains more elements than $C$ then $S(B)&gt;S(C)$.</li>
</ol>
If $S(A)$ is minimised for a given $n$, we shall call it an optimum special sum set. The first five optimum special sum sets are given below.
$n = 1: \{1\}$<br>$n = 2: \{1, 2\}$<br>$n = 3: \{2, 3, 4\}$<br>$n = 4: \{3, 5, 6, 7\}$<br>$n = 5: \{6, 9, 11, 12, 13\}$
It <i>seems</i> that for a given optimum set, $A = \{a_1, a_2, \dots , a_n\}$, the next optimum set is of the form $B = \{b, a_1+b, a_2+b, \dots ,a_n+b\}$, where $b$ is the “middle” element on the previous row.
By applying this “rule” we would expect the optimum set for $n = 6$ to be $A = \{11, 17, 20, 22, 23, 24\}$, with $S(A) = 117$. However, this is not the optimum set, as we have merely applied an algorithm to provide a near optimum set. The optimum set for $n = 6$ is $A = \{11, 18, 19, 20, 22, 25\}$, with $S(A) = 115$ and corresponding set string: $111819202225$.
Given that $A$ is an optimum special sum set for $n = 7$, find its set string.
NOTE: This problem is related to <a href="/105">Problem 105</a> and <a href="/106">Problem 106</a>.


## 解决方案


## 代码


