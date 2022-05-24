---
title: Project Euler 720
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 720
## 题目
### Unpredictable Permutations

Consider all permutations of $\{1, 2, \ldots N\}$, listed in lexicographic order.<br />For example, for $N=4$, the list starts as follows:
<div>
$$\displaylines{
(1, 2, 3, 4) \\
(1, 2, 4, 3) \\
(1, 3, 2, 4) \\
(1, 3, 4, 2) \\
(1, 4, 2, 3) \\
(1, 4, 3, 2) \\
(2, 1, 3, 4) \\
\vdots
}$$
</div>

Let us call a permutation $P$ <i>unpredictable</i> if there is no choice of three indices $i \lt j \lt k$ such that $P(i)$, $P(j)$ and $P(k)$ constitute an arithmetic progression.<br /> For example, $P=(3, 4, 2, 1)$ is <i>not</i> unpredictable because $P(1), P(3), P(4)$ is an arithmetic progression.


Let $S(N)$ be the position within the list of the first unpredictable permutation.



For example, given $N = 4$, the first unpredictable permutation is $(1, 3, 2, 4)$ so $S(4) = 3$.<br />
You are also given that $S(8) = 2295$ and $S(32) \equiv 641839205 \pmod{1\,000\,000\,007}$.


Find $S(2^{25})$. Give your answer modulo $1\,000\,000\,007$.



# Project Euler 720
## 题目
### Unpredictable Permutations

Consider all permutations of ${1, 2, \ldots N}$, listed in lexicographic order.<br>For example, for $N=4$, the list starts as follows:
$$\displaylines{<br>(1, 2, 3, 4) \<br>(1, 2, 4, 3) \<br>(1, 3, 2, 4) \<br>(1, 3, 4, 2) \<br>(1, 4, 2, 3) \<br>(1, 4, 3, 2) \<br>(2, 1, 3, 4) \<br>\vdots<br>}$$
Let us call a permutation $P$ <i>unpredictable</i> if there is no choice of three indices $i \lt j \lt k$ such that $P(i)$, $P(j)$ and $P(k)$ constitute an arithmetic progression.<br>For example, $P=(3, 4, 2, 1)$ is <i>not</i> unpredictable because $P(1), P(3), P(4)$ is an arithmetic progression.
Let $S(N)$ be the position within the list of the first unpredictable permutation.
For example, given $N = 4$, the first unpredictable permutation is $(1, 3, 2, 4)$ so $S(4) = 3$.<br>You are also given that $S(8) = 2295$ and $S(32) \equiv 641839205 \pmod{1\ 000\ 000\ 007}$.
Find $S(2^{25})$. Give your answer modulo $1\ 000\ 000\ 007$.


## 解决方案


## 代码


