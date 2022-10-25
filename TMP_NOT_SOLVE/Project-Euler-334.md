---
title: Project Euler 334
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 334
## 题目
### Spilling the beans


In Plato's heaven, there exist an infinite number of bowls in a straight line.<br />
Each bowl either contains some or none of a finite number of beans.<br />
A child plays a game, which allows only one kind of move: removing two beans from any bowl, and putting one in each of the two adjacent bowls.<br /> The game ends when each bowl contains either one or no beans.

For example, consider two adjacent bowls containing 2 and 3 beans respectively, all other bowls being empty. The following eight moves will finish the game:

<div align="center"><img src="project/images/p334_beans.gif" class="dark_img" alt="p334_beans.gif" /></div>

You are given the following sequences:<br />


$\def\htmltext#1{\style{font-family:inherit;}{\text{#1}}}$
$
\begin{align}
\qquad t_0 &amp;= 123456,\cr
\qquad t_i &amp;= \cases{
\;\;\frac{t_{i-1}}{2},&amp;$\htmltext{if }t_{i-1}\htmltext{ is even}$\cr
\left\lfloor\frac{t_{i-1}}{2}\right\rfloor\oplus 926252,&amp;$\htmltext{if }t_{i-1}\htmltext{ is odd}$\cr}\cr
&amp;\qquad\htmltext{where }\lfloor x\rfloor\htmltext{ is the floor function }\cr
&amp;\qquad\!\htmltext{and }\oplus\htmltext{is the bitwise XOR operator.}\cr
\qquad b_i &amp;= (t_i\bmod2^{11}) + 1.\cr
\end{align}
$


The first two terms of the last sequence are $b_1 = 289$ and $b_2 = 145$.<br />
If we start with $b_1$ and $b_2$ beans in two adjacent bowls, $3419100$ moves would be required to finish the game.

Consider now $1500$ adjacent bowls containing $b_1, b_2, \ldots, b_{1500}$ beans respectively, all other bowls being empty. Find how many moves it takes before the game ends.


# Project Euler 334
## 题目
### Spilling the beans

In Plato’s heaven, there exist an infinite number of bowls in a straight line.<br>Each bowl either contains some or none of a finite number of beans.<br>A child plays a game, which allows only one kind of move: removing two beans from any bowl, and putting one in each of the two adjacent bowls.<br>The game ends when each bowl contains either one or no beans.
For example, consider two adjacent bowls containing 2 and 3 beans respectively, all other bowls being empty. The following eight moves will finish the game:
<center><img src="https://projecteuler.net/project/images/p334_beans.gif"></center>

You are given the following sequences:
$t_0=123456.$
$t_i=\frac{t_{i-1}}{2}$, if $t_{i-1}$ is even<br>$t_i=\lfloor \frac{t_{i-1}}{2} \rfloor \oplus 926252$, if $t_{i-1}$ is odd<br>where $\lfloor x \rfloor$ is the floor function<br>and $\oplus$ is the bitwise XOR operator.
$b_i=(t_i \text{ mod } 2^11) + 1.$
The first two terms of the last sequence are b_<i>1</i> = 289 and b_<i>2</i> = 145.<br>If we start with b_<i>1</i> and b_<i>2</i> beans in two adjacent bowls, 3419100 moves would be required to finish the game.
Consider now 1500 adjacent bowls containing b_<i>1</i>, b_<i>2</i>,\dots, b_<i>1500</i> beans respectively, all other bowls being empty. Find how many moves it takes before the game ends.


## 解决方案


## 代码


