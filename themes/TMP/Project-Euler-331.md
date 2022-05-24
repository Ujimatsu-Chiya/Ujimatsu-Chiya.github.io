---
title: Project Euler 331
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 331
## 题目
### Cross flips

<var>N</var>\times<var>N</var> disks are placed on a square game board. Each disk has a black side and white side.

At each turn, you may choose a disk and flip all the disks in the same row and the same column as this disk: thus 2\times<var>N</var>-1 disks are flipped. The game ends when all disks show their white side. The following example shows a game on a 5\times5 board.

<div align="center"><img src="project/images/p331_crossflips3.gif" alt="p331_crossflips3.gif" /></div>

It can be proven that 3 is the minimal number of turns to finish this game.

The bottom left disk on the <var>N</var>\times<var>N</var> board has coordinates (0,0);<br />
the bottom right disk has coordinates (<var>N</var>-1,0) and the top left disk has coordinates (0,<var>N</var>-1). 

Let C_<var>N</var> be the following configuration of a board with <var>N</var>\times<var>N</var> disks:<br />
A disk at (<var>x</var>,<var>y</var>) satisfying $N - 1 \le \sqrt{x^2 + y^2} \lt N$, shows its black side; otherwise, it shows its white side. C_5 is shown above.

Let T(<var>N</var>) be the minimal number of turns to finish a game starting from configuration C_<var>N</var> or 0 if configuration C_<var>N</var> is unsolvable.<br />
We have shown that T(5)=3. You are also given that T(10)=29 and T(1 000)=395253.

Find $\sum \limits_{i = 3}^{31} {T(2^i - i)}$.



# Project Euler 331
## 题目
### Cross flips

N\timesN disks are placed on a square game board. Each disk has a black side and white side.
At each turn, you may choose a disk and flip all the disks in the same row and the same column as this disk: thus 2\timesN-1 disks are flipped. The game ends when all disks show their white side. The following example shows a game on a 5\times5 board.
<center><img src="https://projecteuler.net/project/images/p331_crossflips3.gif"></center>

It can be proven that 3 is the minimal number of turns to finish this game.
The bottom left disk on the N\timesN board has coordinates (0,0);<br>the bottom right disk has coordinates (N-1,0) and the top left disk has coordinates (0,N-1). 
Let C_N be the following configuration of a board with N\timesN disks:<br>A disk at (x,y) satisfying $N-1 \le \sqrt{x^2+y^2} \lt N$, shows its black side; otherwise, it shows its white side. C_5 is shown above.
Let T(N) be the minimal number of turns to finish a game starting from configuration C_N or 0 if configuration C_N is unsolvable.<br>We have shown that T(5)=3. You are also given that T(10)=29 and T(1 000)=395253.
Find $\sum_{i=3}^{31}T(2^i-1)$.


## 解决方案


## 代码


