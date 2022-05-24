---
title: Project Euler 212
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    


# Project Euler 212
## 题目
### Combined Volume of Cuboids

An *axis-aligned cuboid*, specified by parameters $\{ (x_0,y_0,z_0), (dx,dy,dz) \}$, consists of all points $(X,Y,Z)$ such that $x_0 \le X \le x_0+dx, y_0 \le Y \le y_0+dy$ and $z_0 \le Z \le z_0+dz$.  The volume of the cuboid is the product, $dx \times dy \times dz$.  The *combined volume* of a collection of cuboids is the volume of their union and will be less than the sum of the individual volumes if any cuboids overlap.

Let $C_1,\dots,C_{50000}$ be a collection of $50000$ axis-aligned cuboids such that $C_n$ has parameters

$\begin{aligned}
x_0 &=& S_{6n-5} \text{ modulo } 10000\\
y_0 &=& S_{6n-4} \text{ modulo } 10000\\
z_0 &=& S_{6n-3} \text{ modulo } 10000\\
dx &=& 1 + (S_{6n-2} \text{ modulo } 399)\\
dy &=& 1 + (S_{6n-1} \text{ modulo } 399)\\
dz &=& 1 + (S_{6n} \text{ modulo } 399)
\end{aligned}$

where $S_1,\dots,S_300000$ come from the “Lagged Fibonacci Generator”:

For $1 \le k \le 55, S_k = [100003 - 200003k + 300007k^3]  (\text{ modulo } 1000000)$

For $56 \le k, S_k = [S_{k-24} + S_{k-55}] (\text{ modulo } 1000000)$

Thus, $C_1$ has parameters $\{(7,53,183),(94,369,56)\}$, $C_2$ has parameters $\{(2383,3563,5079),(42,212,344)\}$, and so on.

The combined volume of the first $100$ cuboids, $C_1,\dots,C_{100}$, is $723581599$.

What is the combined volume of all $50000$ cuboids, $C_1,\dots,C_{50000}$ ?


## 解决方案


## 代码


