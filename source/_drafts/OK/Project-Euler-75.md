---
title: Project Euler 75
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 75
## 题目
### Singular integer right triangles
It turns out that $12 \mathrm{cm}$ is the smallest length of wire that can be bent to form an integer sided right angle triangle in exactly one way, but there are many more examples.

$\begin{aligned}
& \mathbf{12cm}: (3,4,5) \\
& \mathbf{24cm}: (6,8,10) \\
& \mathbf{30cm}: (5,12,13) \\
& \mathbf{36cm}: (9,12,15) \\
& \mathbf{40cm}: (8,15,17) \\
& \mathbf{48cm}: (12,16,20)
\end{aligned}$

In contrast, some lengths of wire, like $20 \mathrm{cm}$, cannot be bent to form an integer sided right angle triangle, and other lengths allow more than one solution to be found; for example, using $120 \mathrm{cm}$ it is possible to form exactly three different integer sided right angle triangles.

$$\mathbf{120cm}: (30,40,50), (20,48,52), (24,45,51)$$

Given that $L$ is the length of the wire, for how many values of $L \leq 1,500,000$ can exactly one integer sided right angle triangle be formed?