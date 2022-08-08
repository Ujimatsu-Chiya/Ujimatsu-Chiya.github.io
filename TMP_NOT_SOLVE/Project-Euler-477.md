---
title: Project Euler 477
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 477
## 题目
### Number Sequence Game


The number sequence game starts with a sequence <var>S</var> of <var>N</var> numbers written on a line.
Two players alternate turns. The players on their respective turns must select and remove either the first or the last number remaining in the sequence.
A player's own score is (determined by) the sum of all the numbers that player has taken. Each player attempts to maximize their own sum.
If <var>N</var> = 4 and <var>S</var> = {1, 2, 10, 3}, then each player maximizes their own score as follows:
<ul><li>Player 1: removes the first number (1)</li>
<li>Player 2: removes the last number from the remaining sequence (3)</li>
<li>Player 1: removes the last number from the remaining sequence (10)</li>
<li>Player 2: removes the remaining number (2)</li>
</ul>Player 1 score is 1 + 10 = 11.
Let <var>F</var>(<var>N</var>) be the score of player 1 if both players follow the optimal strategy for the sequence <var>S</var> = {<var>s</var>_1, <var>s</var>_2, \dots, <var>s_N</var>} defined as:
<ul><li><var>s</var>_1 = 0</li>
<li><var>s</var>_<var>i</var>+1 = (<var>s_i</var>^2 + 45) modulo 1 000 000 007</li>
</ul>The sequence begins with <var>S</var> = {0, 45, 2070, 4284945, 753524550, 478107844, 894218625, \dots}.
You are given <var>F</var>(2) = 45, <var>F</var>(4) = 4284990, <var>F</var>(100) = 26365463243, <var>F</var>(10^4) = 2495838522951.
Find <var>F</var>(10^8).


# Project Euler 477
## 题目
### Number Sequence Game

The number sequence game starts with a sequence S of N numbers written on a line.
Two players alternate turns. At his turn, a player must select and remove either the first or the last number remaining in the sequence.
The player score is the sum of all the numbers he has taken. Each player attempts to maximize his own sum.
If N = 4 and S = {1, 2, 10, 3}, then each player maximizes his score as follows:
<ul>
<li>Player 1: removes the first number (1)</li>
<li>Player 2: removes the last number from the remaining sequence (3)</li>
<li>Player 1: removes the last number from the remaining sequence (10)</li>
<li>Player 2: removes the remaining number (2)</li>
</ul>
Player 1 score is 1 + 10 = 11.
Let F(N) be the score of player 1 if both players follow the optimal strategy for the sequence S = {s_1, s_2,&nbsp;\dots,&nbsp;s_N} defined as:
<ul>
<li>s_1 = 0</li>
<li>s_i+1 = (s_i^2 + 45) modulo 1 000 000 007</li>
</ul>
The sequence begins with S&nbsp;=&nbsp;{0,&nbsp;45,&nbsp;2070,&nbsp;4284945,&nbsp;753524550,&nbsp;478107844,&nbsp;894218625,&nbsp;\dots\dots}.
You are given F(2)&nbsp;=&nbsp;45, F(4)&nbsp;=&nbsp;4284990, F(100)&nbsp;=&nbsp;26365463243, F(10^4)&nbsp;=&nbsp;2495838522951.
Find F(10^8).


## 解决方案


## 代码


