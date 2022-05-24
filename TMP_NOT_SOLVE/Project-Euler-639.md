---
title: Project Euler 639
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 639
## 题目
### Summing a multiplicative function

A <b>multiplicative function</b> $f(x)$ is a function over positive integers satisfying $f(1)=1$ and $f(a b)=f(a) f(b)$ for any two coprime positive integers $a$ and $b$.

For integer $k$ let $f_k(n)$ be a multiplicative function additionally satisfying $f_k(p^e)=p^k$ for any prime $p$ and any integer $e>0$.<br /> 
For example, $f_1(2)=2$, $f_1(4)=2$, $f_1(18)=6$ and $f_2(18)=36$.

Let $\displaystyle S_k(n)=\sum_{i=1}^{n} f_k(i)$.
For example, $S_1(10)=41$, $S_1(100)=3512$, $S_2(100)=208090$, $S_1(10000)=35252550$ and $\displaystyle \sum_{k=1}^{3} S_k(10^{8}) \equiv 338787512 \pmod{ 1\,000\,000\,007}$.

Find $\displaystyle \sum_{k=1}^{50} S_k(10^{12}) \bmod 1\,000\,000\,007$.



# Project Euler 639
## 题目
### Summing a multiplicative function

A **multiplicative function** $f(x)$ is a function over positive integers satisfying $f(1)=1$ and $f(ab)=f(a)f(b)$ for any two coprime positive integers $a$ and $b$.
For integer $k$ let $f_k(n)$ be a multiplicative function additionally satisfying $f_k(e^p)=p^k$ for any prime $p$ and any integer $e>0$.<br>For example, $f_1(2)=2$, $f_1(4)=2$, $f_1(18)=6$ and $f_2(18)=36$.
Let $S_k(n)=\sum_{i=1}^n f_k(i)$. For example, $S_1(10)=41$, $S_1(100)=3512$, $S_2(100)=208090$, $S_1(10000)=35252550$ and $\sum_{k=1}^3 S_k(10^8)\equiv 338787512 (\mod 1\ 000\ 000\ 007)$. 
Find $\sum_{k=1}^{50}S_k(10^{12})\mod 1\ 000\ 000\ 007$.


## 解决方案


## 代码


