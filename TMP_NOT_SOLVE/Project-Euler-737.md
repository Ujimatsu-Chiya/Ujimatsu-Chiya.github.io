---
title: Project Euler 737
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 737
## 题目
### Coin Loops


A game is played with many identical, round coins on a flat table.


Consider a line perpendicular to the table.<br />
The first coin is placed on the table touching the line.<br />
Then, one by one, the coins are placed horizontally on top of the previous coin and touching the line.<br />
The complete stack of coins must be balanced after every placement.


The diagram below [not to scale] shows a possible placement of 8 coins where point $P$ represents the line.

<div style="text-align:center;">
<img src="project/images/p737_coinloop.jpg" class="dark_img" alt="" /></div>

It is found that a minimum of $31$ coins are needed to form a <i>coin loop</i> around the line, i.e. if in the projection of the coins on the table the centre of the $n$th coin is rotated $\theta_n$, about the line, from the centre of the $(n-1)$th coin then the sum of $\displaystyle\sum_{k=2}^n \theta_k$ is first larger than $360^\circ$ when $n=31$. In general, to loop $k$ times, $n$ is the smallest number for which the sum is greater than $360^\circ k$.


Also, $154$ coins are needed to loop two times around the line, and $6947$ coins to loop ten times.


Calculate the number of coins needed to loop $2020$ times around the line.



# Project Euler 737
## 题目
### Coin Loops

A game is played with many identical, round coins on a flat table.
Consider a line perpendicular to the table.<br>The first coin is placed on the table touching the line.<br>Then, one by one, the coins are placed horizontally on top of the previous coin and touching the line.<br>The complete stack of coins must be balanced after every placement.
The diagram below [not to scale] shows a possible placement of $8$ coins where point $P$ represents the line.
<img src="https://projecteuler.net/project/images/p737_coinloop.jpg" alt="">
It is found that a minimum of $31$ coins are needed to form a <i>coin loop</i> around the line, i.e. if in the projection of the coins on the table the centre of the $n$th coin is rotated $\theta_n$, about the line, from the centre of the $(n-1)$th coin then the sum of $\displaystyle\sum_{k=2}^n \theta_k$ is first larger than $360^\circ$ when $n=31$. In general, to loop $k$ times, $n$ is the smallest number for which the sum is greater than $360^\circ k$.
Also, $154$ coins are needed to loop two times around the line, and $6947$ coins to loop ten times.
Calculate the number of coins needed to loop $2020$ times around the line.


## 解决方案


## 代码


