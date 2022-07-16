---
title: Project Euler 806
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 806
## 题目
### Nim on Towers of Hanoi

This problem combines the game of Nim with the Towers of Hanoi. For a brief introduction to the rules of these games, please refer to <a href="problem=301">Problem 301</a> and <a href="problem=497">Problem 497</a>, respectively.

The unique shortest solution to the Towers of Hanoi problem with $n$ disks and $3$ pegs requires $2^n-1$ moves. Number the positions in the solution from index 0 (starting position, all disks on the first peg) to index $2^n-1$ (final position, all disks on the third peg).

Each of these $2^n$ positions can be considered as the starting configuration for a game of Nim, in which two players take turns to select a peg and remove any positive number of disks from it. The winner is the player who removes the last disk.

We define $f(n)$ to be the sum of the indices of those positions for which, when considered as a Nim game, the first player will lose (assuming an optimal strategy from both players).

For $n=4$, the indices of losing positions in the shortest solution are 3,6,9 and 12. So we have $f(4) = 30$.

You are given that $f(10) = 67518$.

Find $f(10^5)$. Give your answer modulo $1\,000\,000\,007$.


## 解决方案


## 代码


