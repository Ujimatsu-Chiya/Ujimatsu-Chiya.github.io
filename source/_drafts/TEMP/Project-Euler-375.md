---
title: Project Euler 375
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 375
## 题目
### Minimum of subsequences

Let $S_n$ be an integer sequence produced with the following pseudo-random number generator:
\[
\begin{equation}
\begin{split}
S_0 &amp; = 290797 \\
S_{n+1} &amp; = S_n^2 \bmod 50515093
\end{split}
\end{equation}
\]


Let $A(i, j)$ be the minimum of the numbers $S_i, S_{i+1}, \ldots, S_j$ for $i\le j$.<br />
Let $M(N) = \sum A(i, j)$ for $1 \le i \le j \le N$.<br />
We can verify that $M(10) = 432256955$ and $M(10\,000) = 3264567774119$.


Find $M(2\,000\,000\,000)$.



# Project Euler 375
## 题目
### Minimum of subsequences

Let S_n be an integer sequence produced with the following pseudo-random number generator:
$$S_0=290797$$ $$S_{n+1}=S_n^2 \text{ mod } 50515093$$
Let A(i, j) be the minimum of the numbers S_i, S_i+1, \dots , S_j for i \le j.<br>Let M(N) = \sumA(i, j) for 1 \le i \le j \le N.<br>We can verify that M(10) = 432256955 and M(10 000) = 3264567774119.
Find M(2 000 000 000).


## 解决方案


## 代码


