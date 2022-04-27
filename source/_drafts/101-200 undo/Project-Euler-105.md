---
title: Project Euler 105
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 105
## 题目
### Special subset sums: testing

Let S(A) represent the sum of elements in set A of size <i>n</i>. We shall call it a special sum set if for any two non-empty disjoint subsets, B and C, the following properties are true:
<ol><li>S(B) ≠ S(C); that is, sums of subsets cannot be equal.</li>
<li>If B contains more elements than C then S(B) &gt; S(C).</li>
</ol>For example, {81, 88, 75, 42, 87, 84, 86, 65} is not a special sum set because 65 + 87 + 88 = 75 + 81 + 84, whereas {157, 150, 164, 119, 79, 159, 161, 139, 158} satisfies both rules for all possible subset pair combinations and S(A) = 1286.
Using <a href="project/resources/p105_sets.txt">sets.txt</a> (right click and "Save Link/Target As\dots"), a 4K text file with one-hundred sets containing seven to twelve elements (the two examples given above are the first two sets in the file), identify all the special sum sets, A_1, A_2, \dots, A_<i>k</i>, and find the value of S(A_1) + S(A_2) + \dots + S(A_<i>k</i>).
<p class="smaller">NOTE: This problem is related to <a href="problem=103">Problem 103</a> and <a href="problem=106">Problem 106</a>.


# Project Euler 105
## 题目
### Special subset sums: testing
Let $S(A)$ represent the sum of elements in set $A$ of size $n$. We shall call it a special sum set if for any two non-empty disjoint subsets, $B$ and $C$, the following properties are true:
<ol>
<li>$S(B)\neq S(C)$; that is, sums of subsets cannot be equal.</li>
<li>If $B$ contains more elements than $C$ then $S(B) &gt; S(C)$.</li>
</ol>
For example, $\{81, 88, 75, 42, 87, 84, 86, 65\}$ is not a special sum set because $65 + 87 + 88 = 75 + 81 + 84$, whereas $\{157, 150, 164, 119, 79, 159, 161, 139, 158\}$ satisfies both rules for all possible subset pair combinations and $S(A) = 1286$.
Using <a href="https://projecteuler.net/project/resources/p105_sets.txt" target="_blank" rel="noopener">sets.txt</a> (right click and “Save Link/Target As\dots”), a 4K text file with one-hundred sets containing seven to twelve elements (the two examples given above are the first two sets in the file), identify all the special sum sets, $A_1, A_2, \ldots , A_k$, and find the value of $S(A_1) + S(A_2) +\ldots + S(A_k)$.
NOTE: This problem is related to <a href="/103">Problem 103</a> and <a href="/106">Problem 106</a>.


## 解决方案


## 代码


