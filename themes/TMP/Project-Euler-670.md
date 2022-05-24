---
title: Project Euler 670
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 670
## 题目
### Colouring a Strip

A certain type of tile comes in three different sizes - 1\times1, 1\times2, and 1\times3 - and in four different colours: blue, green, red and yellow. There is an unlimited number of tiles available in each combination of size and colour.

These are used to tile a $2\times n$ rectangle, where $n$ is a positive integer, subject to the following conditions:
<ul><li>The rectangle must be fully covered by non-overlapping tiles.</li>
<li>It is <i>not</i> permitted for four tiles to have their corners meeting at a single point.</li>
<li>Adjacent tiles must be of different colours.</li>
</ul>For example, the following is an acceptable tiling of a $2\times 12$ rectangle:

<div class="center">
<img src="project/images/p670_strip_acceptable.png" alt="Acceptable colouring" /></div>

but the following is not an acceptable tiling, because it violates the "no four corners meeting at a point" rule:

<div class="center">
<img src="project/images/p670_strip_unacceptable.png" alt="Unacceptable colouring" /></div>

Let $F(n)$ be the number of ways the $2\times n$ rectangle can be tiled subject to these rules. Where reflecting horizontally or vertically would give a different tiling, these tilings are to be counted separately.

For example, $F(2) = 120$, $F(5) = 45876$, and $F(100)\equiv 53275818 \pmod{1\,000\,004\,321}$.
Find $F(10^{16}) \bmod 1\,000\,004\,321$.




# Project Euler 670
## 题目
### Colouring a Strip

A certain type of tile comes in three different sizes - $1\times 1$, $1\times2$, and $1\times 3$ - and in four different colours: blue, green, red and yellow. There is an unlimited number of tiles available in each combination of size and colour.
These are used to tile a $2\times n$ rectangle, where $n$ is a positive integer, subject to the following conditions:
<ul>
<li>The rectangle must be fully covered by non-overlapping tiles.</li>
<li>It is <i>not</i> permitted for four tiles to have their corners meeting at a single point.</li>
<li>Adjacent tiles must be of different colours.</li>
</ul>
For example, the following is an acceptable tiling of a $2\times 12$ rectangle:
<img src="https://projecteuler.net/project/images/p670_strip_acceptable.png" alt="Acceptable colouring">
but the following is not an acceptable tiling, because it violates the “no four corners meeting at a point” rule:
<img src="https://projecteuler.net/project/images/p670_strip_unacceptable.png" alt="Unacceptable colouring">
Let $F(n)$ be the number of ways the $2\times n$ rectangle can be tiled subject to these rules. Where reflecting horizontally or vertically would give a different tiling, these tilings are to be counted separately.
For example, $F(2) = 120$, $F(5) = 45876$, and $F(100)\equiv 53275818 \pmod{1\ 000\ 004\ 321}$.
Find $F(10^{16}) \bmod 1\ 000\ 004\ 321$.


## 解决方案


## 代码


