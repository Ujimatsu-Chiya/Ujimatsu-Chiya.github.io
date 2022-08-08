---
title: Project Euler 326
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 326
## 题目
### Modulo Summations



Let $a_n$ be a sequence recursively defined by:$\quad a_1=1,\quad\displaystyle a_n=\biggl(\sum_{k=1}^{n-1}k\cdot a_k\biggr)\bmod n$.


So the first 10 elements of $a_n$ are: 1,1,0,3,0,3,5,4,1,9.

Let <var>f</var>(<var>N,M</var>) represent the number of pairs (<var>p,q</var>) such that: 

$$
\def\htmltext#1{\style{font-family:inherit;}{\text{#1}}}
1\le p\le q\le N \quad\htmltext{and}\quad\biggl(\sum_{i=p}^qa_i\biggr)\bmod M=0
$$


It can be seen that <var>f</var>(10,10)=4 with the pairs (3,3), (5,5), (7,9) and (9,10).


You are also given that <var>f</var>(10^4,10^3)=97158.

Find <var>f</var>(10^12,10^6).




 





# Project Euler 326
## 题目
### Modulo Summations

Let a_n be a sequence recursively defined by: $a_1=1, a_n=(\sum_{k=1}^{n-1}k·a_k) \text{ mod } n$.
So the first 10 elements of a_n are: 1,1,0,3,0,3,5,4,1,9.
Let f(N,M) represent the number of pairs (p,q) such that: 
$$ 1 \le p \le q \le N \text{ and } (\sum_{t=p}^{q}a_i) \text{ mod } M=0$$
It can be seen that f(10,10)=4 with the pairs (3,3), (5,5), (7,9) and (9,10).
You are also given that f(10^4,10^3)=97158.
Find f(10^12,10^6).


## 解决方案


## 代码


