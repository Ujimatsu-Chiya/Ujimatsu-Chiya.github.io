---
title: Project Euler 775
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 775
## 题目
### Saving Paper

When wrapping several cubes in paper, it is more efficient to wrap them all together than to wrap each one individually. For example, with 10 cubes of unit edge length, it would take 30 units of paper to wrap them in the arrangement shown below, but 60 units to wrap them separately.

<div style="text-align:center;">
<img src="project/images/p775_wrapping_cubes.png" class="dark_img" alt="" /></div>


Define $g(n)$ to be the maximum amount of paper that can be saved by wrapping $n$ identical $1\times 1\times 1$ cubes in a compact arrangement, compared with wrapping them individually. We insist that the wrapping paper is in contact with the cubes at all points, without leaving a void.

With 10 cubes, the arrangement illustrated above is optimal, so $g(10)=60-30=30$. With 18 cubes, it can be shown that the optimal arrangement is as a $3\times 3\times 2$, using 42 units of paper, whereas wrapping individually would use 108 units of paper; hence $g(18) = 66$.

Define
$$G(N) = \sum_{n=1}^N g(n)$$
You are given that $G(18) = 530$, and $G(10^6) \equiv 951640919 \pmod {1\,000\,000\,007}$.

Find $G(10^{16})$. Give your answer modulo $1\,000\,000\,007$.


## 解决方案


## 代码


