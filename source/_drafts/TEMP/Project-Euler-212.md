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

An <span style="font-style:italic;">axis-aligned cuboid</span>, specified by parameters { (x_0,y_0,z_0), (dx,dy,dz) }, consists of all points (X,Y,Z) such that x_0 \le X \le x_0+dx, y_0 \le Y \le y_0+dy and z_0 \le Z \le z_0+dz.  The volume of the cuboid is the product, dx \times dy \times dz.  The <span style="font-style:italic;">combined volume</span> of a collection of cuboids is the volume of their union and will be less than the sum of the individual volumes if any cuboids overlap.

Let C_1,\dots,C_50000 be a collection of 50000 axis-aligned cuboids such that C_<var>n</var> has parameters

<p style="margin-left:40px;">x_0 = S_6<var>n</var>-5 modulo 10000<br />y_0 = S_6<var>n</var>-4 modulo 10000<br />z_0 = S_6<var>n</var>-3 modulo 10000<br />dx = 1 + (S_6<var>n</var>-2 modulo 399)<br />dy = 1 + (S_6<var>n</var>-1 modulo 399)<br />dz = 1 + (S_6<var>n</var> modulo 399)

where S_1,\dots,S_300000 come from the "Lagged Fibonacci Generator":

<p style="margin-left:40px;">For 1 \le <var>k</var> \le 55, S_<var>k</var> = [100003 - 200003<var>k</var> + 300007<var>k</var>^3]   (modulo 1000000)<br />For 56 \le <var>k</var>, S_<var>k</var> = [S_<var>k</var>-24 + S_<var>k</var>-55]   (modulo 1000000)

Thus, C_1 has parameters {(7,53,183),(94,369,56)}, C_2 has parameters {(2383,3563,5079),(42,212,344)}, and so on.

The combined volume of the first 100 cuboids, C_1,\dots,C_100, is 723581599.

What is the combined volume of all 50000 cuboids, C_1,\dots,C_50000 ?


# Project Euler 212
## 题目
### Combined Volume of Cuboids

An <i>axis-aligned cuboid</i>, specified by parameters { (x_0,y_0,z_0), (dx,dy,dz) }, consists of all points (X,Y,Z) such that x_0 \le X \le x_0+dx, y_0 \le Y \le y_0+dy and z_0 \le Z \le z_0+dz.  The volume of the cuboid is the product, dx \times dy \times dz.  The <i>combined volume</i> of a collection of cuboids is the volume of their union and will be less than the sum of the individual volumes if any cuboids overlap.
Let C_1,\dots,C_50000 be a collection of 50000 axis-aligned cuboids such that C_n has parameters
x_0 = S_6n-5 modulo 10000<br>y_0 = S_6n-4 modulo 10000<br>z_0 = S_6n-3 modulo 10000<br>dx = 1 + (S_6n-2 modulo 399)<br>dy = 1 + (S_6n-1 modulo 399)<br>dz = 1 + (S_6n modulo 399)
where S_1,\dots,S_300000 come from the “Lagged Fibonacci Generator”:
For 1 \le k \le 55, S_k = [100003 - 200003k + 300007k^3] &nbsp; (modulo 1000000)<br>For 56 \le k, S_k = [S_k-24 + S_k-55] &nbsp; (modulo 1000000)
Thus, C_1 has parameters {(7,53,183),(94,369,56)}, C_2 has parameters {(2383,3563,5079),(42,212,344)}, and so on.
The combined volume of the first 100 cuboids, C_1,\dots,C_100, is 723581599.
What is the combined volume of all 50000 cuboids, C_1,\dots,C_50000 ?


## 解决方案


## 代码


