---
title: Project Euler 167
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 167
## 题目
### Investigating Ulam sequences


For two positive integers a and b, the Ulam sequence U(a,b) is defined by U(a,b)_1 = a, U(a,b)_2 = b and for k &gt; 2,
U(a,b)_k is the smallest integer greater than U(a,b)_(k-1) which can be written in exactly one way as the sum of two distinct previous members of U(a,b).
For example, the sequence U(1,2) begins with<br />
1, 2, 3 = 1 + 2, 4 = 1 + 3, 6 = 2 + 4, 8 = 2 + 6, 11 = 3 + 8;<br />
5 does not belong to it because 5 = 1 + 4 = 2 + 3 has two representations as the sum of two previous members, likewise 7 = 1 + 6 = 3 + 4.
Find <span style="font-size:larger;"><span style="font-size:larger;">∑</span></span> U(2,2<var>n</var>+1)_<var>k</var> for 2 ≤ <var>n</var> ≤10, where <var>k</var> = 10^11.


# Project Euler 167
## 题目
### Investigating Ulam sequences
For two positive integers $a$ and $b$, the Ulam sequence $U(a,b)$ is defined by $U(a,b)_1 = a$, $U(a,b)_2 = b$ and for $k > 2,U(a,b)_k$ is the smallest integer greater than $U(a,b)_{(k-1)}$ which can be written in exactly one way as the sum of two distinct previous members of U(a,b).

For example, the sequence $U(1,2)$ begins with

$1, 2, 3 = 1 + 2, 4 = 1 + 3, 6 = 2 + 4, 8 = 2 + 6, 11 = 3 + 8;$

$5$ does not belong to it because $5 = 1 + 4 = 2 + 3$ has two representations as the sum of two previous members, likewise $7 = 1 + 6 = 3 + 4$.

Find $\sum U(2,2n+1)_k$ for $2 \leq n \leq 10$, where k = $10^{11}$.


## 解决方案


## 代码


