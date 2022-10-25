---
title: Project Euler 811
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 811
## 题目
### Bitwise Recursion



Let $b(n)$ be the largest power of 2 that divides $n$. For example $b(24) = 8$.

Define the recursive function:
\begin{align*}
\begin{split}
A(0) &amp;= 1\\
A(2n) &amp;= 3A(n) + 5A\big(2n - b(n)\big)  \qquad n \gt 0\\
A(2n+1) &amp;= A(n)
\end{split}
\end{align*}
and let $H(t,r) = A\big((2^t+1)^r\big)$.

You are given $H(3,2) = A(81) = 636056$.

Find $H(10^{14}+31,62)$. Give your answer modulo $1\,000\,062\,031$. 

## 解决方案


## 代码


