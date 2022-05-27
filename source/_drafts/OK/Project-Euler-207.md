---
title: Project Euler 207
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 207
## 题目
### Integer partition equations


For some positive integers $k$, there exists an integer partition of the form   $4^t = 2^t + k$, where $4^t, 2^t$ and $k$ are all positive integers and $t$ is a real number.

The first two such partitions are $4^1 = 2^1 + 2$ and $4^{1.5849625\dots} = 2^{1.5849625\dots} + 6$.

Partitions where $t$ is also an integer are called *perfect*.

For any $m \ge 1$ let $P(m)$ be the proportion of such partitions that are perfect with $k \le m$.

Thus $P(6) = 1/2$.

In the following table are listed some values of $P(m)$

$\begin{aligned}
   P(5) &= &1/1 \\
   P(10)& = &1/2 \\
   P(15) &= &2/3 \\
   P(20) &= &1/2 \\
   P(25) &= &1/2 \\
   P(30) &= &2/5 \\
   &\dots&\\
   P(180) &=& 1/4\\
   P(185) &=& 3/13
\end{aligned}$

Find the smallest $m$ for which $P(m) < 1/12345$




