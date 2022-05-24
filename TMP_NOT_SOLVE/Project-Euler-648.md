---
title: Project Euler 648
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 648
## 题目
### Skipping Squares

For some fixed $\rho \in [0, 1]$, we begin a sum $s$ at $0$ and repeatedly apply a process: With probability $\rho$, we add $1$ to $s$, otherwise we add $2$ to $s$.

The process ends when either $s$ is a perfect square or $s$ exceeds $10^{18}$, whichever occurs first. For example, if $s$ goes through $0, 2, 3, 5, 7, 9$, the process ends at $s=9$, and two squares $1$ and $4$ were skipped over.

Let $f(\rho)$ be the expected number of perfect squares skipped over when the process finishes.

It can be shown that the power series for $f(\rho)$ is $\sum_{k=0}^\infty a_k \rho^k$ for a suitable (unique) choice of coefficients $a_k$. Some of the first few coefficients are $a_0=1$, $a_1=0$, $a_5=-18$, $a_{10}=45176$.

Let $F(n) = \sum_{k=0}^n a_k$. You are given that $F(10) = 53964$ and $F(50) \equiv 842418857 \pmod{10^9}$.

Find $F(1000)$, and give your answer modulo $10^9$.



# Project Euler 648
## 题目
### Skipping Squares

For some fixed $\rho\in[0,1]$, we begin a sum $s$ at $0$ and repeatedly apply a process: With probability $\rho$, we add $1$ to $s$, otherwise we add $2$ to $s$.
The process ends when either $s$ is a perfect square or $s$ exceeds $10^{18}$, whichever occurs first. For example, if $s$ goes through $0,2,3,5,7,9$, the process ends at $s=9$, and two squares $1$ and $4$ were skipped over.
Let $f(\rho)$ be the expected number of perfect squares skipped over when the process finishes.
It can be shown that the power series for $f(\rho)$ is $\sum_{k=0}^{\infty}a_k\rho^k$ for a suitable (unique) choice of coefficients $a_k$. Some of the first few coefficients are $a_0=1$,<br>$a_1=0$, $a_5=-18$, $a_{10}=45176$.
Let $F(n)=\sum_{k=0}^na_k$. You are given that $F(10)=53964$ and $F(50)\equiv 842418857\pmod{10^9}$.
Find $F(1000)$, and give your answer modulo $10^9$.


## 解决方案


## 代码

