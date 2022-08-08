---
title: Project Euler 707
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 707
## 题目
### Lights Out



Consider a $w\times h$ grid. A cell is either ON or OFF. When a cell is selected, that cell and all cells connected to that cell by an edge are toggled on-off, off-on. See the diagram for the 3 cases of selecting a corner cell, an edge cell or central cell in a grid that has all cells on (white).

<div class="center">
<img src="project/images/p707_LightsOutPic.jpg" alt="LightsOut" /></div>
The goal is to get every cell to be off simultaneously. This is not possible for all starting states. A state is solvable if, by a process of selecting cells, the goal can be achieved.


Let $F(w,h)$ be the number of solvable states for a $w\times h$ grid. 
You are given $F(1,2)=2$, $F(3,3) = 512$, $F(4,4) = 4096$ and $F(7,11) \equiv 270016253 \pmod{1\,000\,000\,007}$.


Let $f_1=f_2 = 1$ and $f_n=f_{n-1}+f_{n-2}, n \ge 3$ be the Fibonacci sequence and define 
$$ S(w,n) = \sum_{k=1}^n F(w,f_k)$$
You are given $S(3,3) = 32$, $S(4,5) = 1052960$ and $S(5,7) \equiv 346547294 \pmod{1\,000\,000\,007}$.


Find $S(199,199)$. Give your answer modulo $1\,000\,000\,007$.



# Project Euler 707
## 题目
### Lights Out

Consider a $w\times h$ grid. A cell is either ON or OFF. When a cell is selected, that cell and all cells connected to that cell by an edge are toggled on-off, off-on. See the diagram for the $3$ cases of selecting a corner cell, an edge cell or central cell in a grid that has all cells on (white).
<img src="https://projecteuler.net/project/images/p707_LightsOutPic.jpg" alt="LightsOut">
The goal is to get every cell to be off simultaneously. This is not possible for all starting states. A state is solvable if, by a process of selecting cells, the goal can be achieved.
Let $F(w,h)$ be the number of solvable states for a $w\times h$ grid. You are given $F(1,2)=2$, $F(3,3) = 512$, $F(4,4) = 4096$ and $F(7,11) \equiv 270016253 \pmod{1\ 000\ 000\ 007}$.
Let $f_1=f_2 = 1$ and $f_n=f_{n-1}+f_{n-2}, n \ge 3$ be the Fibonacci sequence and define<br>$$ S(w,n) = \sum_{k=1}^n F(w,f_k)$$<br>You are given $S(3,3) = 32$, $S(4,5) = 1052960$ and $S(5,7) \equiv 346547294 \pmod{1\ 000\ 000\ 007}$.
Find $S(199,199)$. Give your answer modulo $1\ 000\ 000\ 007$.


## 解决方案


## 代码


