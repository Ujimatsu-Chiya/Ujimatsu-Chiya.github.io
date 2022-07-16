---
title: Project Euler 771
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 771
## 题目
### Pseudo Geometric Sequences


We define a <i>pseudo-geometric sequence</i> to be a finite sequence $a_0, a_1, \dotsc, a_n$ of positive integers, satisfying the following conditions:
<ul>
<li>$n \geq 4$, i.e. the sequence has at least 5 terms.</li>
<li>$0 < a_0 < a_1 < \dotsc < a_n$, i.e. the sequence is strictly increasing.</li>
<li>$| a_i^2 - a_{i - 1}a_{i + 1} | \le 2$ for $1 \le i \le n-1$.</li>
</ul>

Let $G(N)$ be the number of different pseudo-geometric sequences whose terms do not exceed $N$.<br />
For example, $G(6) = 4$, as the following $4$ sequences give a complete list:
<center>$1, 2, 3, 4, 5 \qquad 1, 2, 3, 4, 6 \qquad 2, 3, 4, 5, 6 \qquad 1, 2, 3, 4, 5, 6$ </center>

Also, $G(10) = 26$, $G(100) = 4710$ and $G(1000) = 496805$.

Find $G(10^{18})$. Give your answer modulo $1\,000\,000\,007$.


## 解决方案


## 代码


