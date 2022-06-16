---
title: Project Euler 208
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 208
## 题目
### Robot Walks

A robot moves in a series of one-fifth circular arcs ($72°$), with a free choice of a clockwise or an anticlockwise arc for each step, but no turning on the spot.

One of $70932$ possible closed paths of $25$ arcs starting northward is

![](../images/p208_robotwalk.gif)

Given that the robot starts facing North, how many journeys of $70$ arcs in length can it take that return it, after the final arc, to its starting position?(Any arc may be traversed multiple times.) 


## 解决方案

本方案只适用于$5$的倍数的情况。

假设$n=\dfrac{70}{5}=14$，那么答案为

$$\sum_{i=0}^n\dfrac{(C_n^i)^5\cdot(n^4-3in^3+4i^2n^2-2ni^3+i^4)}{n^4}$$

## 代码


