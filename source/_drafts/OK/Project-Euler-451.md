---
title: Project Euler 451
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    



# Project Euler 451
## 题目
### Modular inverses

Consider the number $15$.

There are eight positive numbers less than $15$ which are coprime to $15: 1,2, 4, 7, 8, 11, 13, 14$.

The modular inverses of these numbers modulo 15 are: $1, 8, 4, 13, 2, 11, 7, 14$ because

$\begin{aligned}
1 \cdot 1 &\mod 15=1\\
2 \cdot 8=16 &\mod 15=1\\
4 \cdot 4=16 &\mod 15=1\\
7 \cdot 13=91 &\mod 15=1\\
11 \cdot 11=121 &\mod 15=1\\
14 \cdot 14=196 &\mod 15=1
\end{aligned}$

Let $I(n)$ be the largest positive number $m$ smaller than $n-1$ such that the modular inverse of $m$ modulo $n$ equals $m$ itself.

So $I(15)=11$.

Also $I(100)=51$ and $I(7)=1$.

Find $\sum I(n)$ for $3\le n\le2\cdot10^7$


## 解决方案


## 代码


