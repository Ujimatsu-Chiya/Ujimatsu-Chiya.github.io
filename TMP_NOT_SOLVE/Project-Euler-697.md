---
title: Project Euler 697
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 697
## 题目
### Randomly Decaying Sequence


Given a fixed real number $c$, define a random sequence $(X_n)_{n\ge 0}$ by the following random process:
<ul><li>$X_0 = c$ (with probability 1).</li>
<li>For $n>0$, $X_n = U_n X_{n-1}$ where $U_n$ is a real number chosen at random between zero and one, uniformly, and independently of all previous choices $(U_m)_{m<n}$.</li>
</ul>If we desire there to be precisely a 25% probability that $X_{100}<1$, then this can be arranged by fixing $c$ such that $\log_{10} c \approx 46.27$.

Suppose now that $c$ is set to a different value, so that there is precisely a 25% probability that $X_{10\,000\,000}<1$.
Find $\log_{10} c$ and give your answer rounded to two places after the decimal point.



# Project Euler 697
## 题目
### Randomly Decaying Sequence

Given a fixed real number $c$, define a random sequence $(X_n)_{n\ge 0}$ by the following random process:
<ul>
<li>$X_0 = c$ (with probability 1).</li>
<li>For $n>0$, $X_n = U_n X_{n-1}$ where $U_n$ is a real number chosen at random between zero and one, uniformly, and independently of all previous choices $(U_m)_{m<n}$.</li>
</ul>
If we desire there to be precisely a $25%$ probability that $X_{100}<1$, then this can be arranged by fixing $c$ such that $\log_{10} c \approx 46.27$.
Suppose now that $c$ is set to a different value, so that there is precisely a  $25%$ probability that $X_{10\ 000\ 000}<1$.
Find $\log_{10} c$ and give your answer rounded to two places after the decimal point.


## 解决方案


## 代码


