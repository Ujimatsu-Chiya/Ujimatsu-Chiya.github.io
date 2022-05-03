---
title: Project Euler 183
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>




# Project Euler 183
## 题目
### Maximum product of parts

Let $N$ be a positive integer and let $N$ be split into $k$ equal parts, $r = \dfrac{N}{k}$, so that $N = r + r + \dots + r$.

Let $P$ be the product of these parts, $P = r × r × \dots × r = r^k$.


For example, if $11$ is split into five equal parts, $11 = 2.2 + 2.2 + 2.2 + 2.2 + 2.2$, then $P = 2.2^5 = 51.53632$.

Let $M(N) = P_max$ for a given value of $N$.

It turns out that the maximum for $N = 11$ is found by splitting eleven into four equal parts which leads to $P_{\max} = (\dfrac{11}{4})^4$; that is, $M(11) = \dfrac{14641}{256} = 57.19140625$, which is a terminating decimal.

However, for $N = 8$ the maximum is achieved by splitting it into three equal parts, so $M(8) = \dfrac{512}{27}$, which is a non-terminating decimal.

Let $D(N) = N$ if $M(N)$ is a non-terminating decimal and $D(N) = -N$ if $M(N)$ is a terminating decimal.

For example, $\sum D(N)$ for $5 \le N \le 100$ is $2438$.

Find $\sum D(N)$ for $5 \le N \le 10000$.


## 解决方案


## 代码


