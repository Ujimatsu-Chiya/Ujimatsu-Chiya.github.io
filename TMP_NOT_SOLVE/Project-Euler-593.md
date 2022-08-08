---
title: Project Euler 593
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 593
## 题目
### Fleeting Medians


We define two sequences $S = \{S(1), S(2), \dots, S(n)\}$ and $S_2 = \{S_2(1), S_2(2), \dots, S_2(n)\}$:

$S(k) = (p_k)^k$ mod $10007$ where $p_k$ is the $k$th prime number.

$S_2(k) = S(k) + S(\lfloor\frac{k}{10000}\rfloor + 1)$ where $\lfloor \cdot \rfloor$ denotes the floor function.

Then let $M(i, j)$ be the median of elements $S_2(i)$ through $S_2(j)$, inclusive. For example, $M(1, 10) = 2021.5$ and $M(10^2, 10^3) = 4715.0$.

Let $F(n, k) = \sum_{i=1}^{n-k+1} M(i, i + k - 1)$. For example, $F(100, 10) = 463628.5$ and $F(10^5, 10^4) = 675348207.5$.

Find $F(10^7, 10^5)$. If the sum is not an integer, use $.5$ to denote a half. Otherwise, use $.0$ instead.


# Project Euler 593
## 题目
### Fleeting Medians

We define two sequences $S = {S(1), S(2), \dots, S(n)}$ and $S_2 = {S_2(1), S_2(2), \dots, S_2(n)}$:
$S(k) = (p_k)^k$ mod $10007$ where $p_k$ is the $k$th prime number.
$S_2(k) = S(k) + S(\lfloor\frac{k}{10000}\rfloor + 1)$ where $\lfloor \cdot \rfloor$ denotes the floor function.
Then let $M(i, j)$ be the median of elements $S_2(i)$ through $S_2(j)$, inclusive. For example, $M(1, 10) = 2021.5$ and $M(10^2, 10^3) = 4715.0$.
Let $F(n, k) = \sum_{i=1}^{n-k+1} M(i, i + k - 1)$. For example, $F(100, 10) = 463628.5$ and $F(10^5, 10^4) = 675348207.5$.
Find $F(10^7, 10^5)$. If the sum is not an integer, use $.5$ to denote a half. Otherwise, use $.0$ instead.


## 解决方案


## 代码


