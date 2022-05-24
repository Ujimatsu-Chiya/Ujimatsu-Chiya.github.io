---
title: Project Euler 459
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 459
## 题目
### Flipping game

The flipping game is a two player game played on a N by N square board.<br />
Each square contains a disk with one side white and one side black.<br />
The game starts with all disks showing their white side.

A turn consists of flipping all disks in a rectangle with the following properties:
<ul><li>the upper right corner of the rectangle contains a white disk</li>
<li>the rectangle width is a perfect square (1, 4, 9, 16, \dots)</li>
<li>the rectangle height is a <dfn title="The triangular numbers are defined as ½ n(n + 1) for positive integer n.">triangular number</dfn> (1, 3, 6, 10, \dots)</li>
</ul><p class="center"><img src="project/images/p459-flipping-game-0.png" alt="p459-flipping-game-0.png" />

Players alternate turns. A player wins by turning the grid all black.

Let W(N) be the number of <dfn title="The first move of a strategy that ensures a win no matter what the opponent plays.">winning moves</dfn> for the first player on a N by N board with all disks white, assuming perfect play.<br />
W(1) = 1, W(2) = 0, W(5) = 8 and W(10^2) = 31395.

For N=5, the first player's eight winning first moves are:

<p class="center"><img src="project/images/p459-flipping-game-1.png" class="dark_img" alt="p459-flipping-game-1.png" />

Find W(10^6).



# Project Euler 459
## 题目
### Flipping game

The flipping game is a two player game played on a N by N square board.<br>Each square contains a disk with one side white and one side black.<br>The game starts with all disks showing their white side.
A turn consists of flipping all disks in a rectangle with the following properties:
<ul>
<li>the upper right corner of the rectangle contains a white disk</li>
<li>the rectangle width is a perfect square (1, 4, 9, 16, \dots)</li>
<li>the rectangle height is a <dfn title="The triangular numbers are defined as ½&nbsp;n(n + 1) for positive integer n.">triangular number</dfn> (1, 3, 6, 10, \dots)</li>
</ul>
<center><img src="https://projecteuler.net/project/images/p459-flipping-game-0.png"></center>

Players alternate turns. A player wins by turning the grid all black.
Let W(N) be the number of <dfn title="The first move of a strategy that ensures a win no matter what the opponent plays.">winning moves</dfn> for the first player on a N by N board with all disks white, assuming perfect play.<br>W(1) = 1, W(2) = 0, W(5) = 8 and W(10^2) = 31395.
For N=5, the first player’s eight winning first moves are:
<center><img src="https://projecteuler.net/project/images/p459-flipping-game-1.png"></center>
<center><img src="https://projecteuler.net/project/images/p459-flipping-game-2.png"></center>

Find W(10^6).


## 解决方案


## 代码


