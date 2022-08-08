---
title: Project Euler 507
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 507
## 题目
### Shortest Lattice Vector



Let $t_n$ be the <b>tribonacci numbers</b> defined as:<br />
$t_0 = t_1 = 0$;<br />
$t_2 = 1$;<br />
$t_n = t_{n-1} + t_{n-2} + t_{n-3}$ for $n \ge 3$<br />
and let $r_n = t_n \text{ mod } 10^7$.


For each pair of Vectors $V_n=(v_1,v_2,v_3)$ and $W_n=(w_1,w_2,w_3)$ with $v_1=r_{12n-11}-r_{12n-10}, v_2=r_{12n-9}+r_{12n-8}, v_3=r_{12n-7} \cdot r_{12n-6}$  and <br /> $w_1=r_{12n-5}-r_{12n-4}, w_2=r_{12n-3}+r_{12n-2}, w_3=r_{12n-1} \cdot r_{12n}$
<br />

we define $S(n)$ as the minimal value of the manhattan length of the vector $D=k \cdot V_n+l \cdot W_n$ measured as $|k \cdot v_1+l \cdot w_1|+|k \cdot v_2+l \cdot w_2|+|k \cdot v_3+l \cdot w_3|$
 for any integers $k$ and $l$ with $(k,l)\neq (0,0)$.

The first vector pair  is (-1, 3, 28), (-11, 125, 40826).<br />
You are given that $S(1)=32$ and $\sum_{n=1}^{10} S(n)=130762273722$.


Find $\sum_{n=1}^{20000000} S(n)$.




# Project Euler 507
## 题目
### Shortest Lattice Vector

Let $t_n$ be the tribonacci numbers defined as:<br>$t_0=t_1=0$;<br>$t_2=1$;<br>$t_n=t_{n-1}+t_{n-2}+t_{n-3}$ for $n\ge3$<br>and let $r_n=t_n \text{ mod } 10^7$.
For each pair of Vectors $V_n=(v_1,v_2,v_3)$ and $W_n=(w_1,w_2,w_3)$ with<br>$v_1=r_{12n-11}-r_{12n-10},v_2=r_{12n-9}+r_{12n-8},v_3=r_{12n-7}·r_{12n-6}$ and<br>$w_1=r_{12n-5}-r_{12n-4},w_2=r_{12n-3}+r_{12n-2},w_3=r_{12n-1}·r_{12n}$<br>we define $S(n)$ as the minimal value of the manhattan length of the vector $D=k·V_n+l·W_n$ measured as<br>$|k·v_1+l·w_1|+|k·v_2+l·w_2|+|k·v_3+l·w_3|$<br>for any integers $k$ and $l$ with $(k,l)≠(0,0)$.
The first vector pair is (-1, 3, 28), (-11, 125, 40826).<br>You are given that $S(1)=32$ and $\Sigma^{10}_{n=1}S(n)=130762273722$.
Find $\Sigma^{20000000}_{n=1}S(n)$.


## 解决方案


## 代码


