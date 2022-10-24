---
title: Project Euler 391
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 391
## 题目
### Hopping Game


Let $s_k$ be the number of 1’s when writing the numbers from 0 to $k$ in binary.<br />
For example, writing 0 to 5 in binary, we have $0, 1, 10, 11, 100, 101$. There are seven 1’s, so $s_5 = 7$.<br />
The sequence $S = \{s_k : k \ge 0\}$ starts $\{0, 1, 2, 4, 5, 7, 9, 12, \dots\}$.

A game is played by two players. Before the game starts, a number $n$ is chosen. A counter $c$ starts at 0. At each turn, the player chooses a number from 1 to $n$ (inclusive) and increases $c$ by that number. The resulting value of $c$ must be a member of $S$. If there are no more valid moves, then the player loses.

For example, with $n = 5$ and starting with $c = 0$:
Player 1 chooses 4, so $c$ becomes $0 + 4 = 4$.<br />
Player 2 chooses 5, so $c$ becomes $4 + 5 = 9$.<br />
Player 1 chooses 3, so $c$ becomes $9 + 3 = 12$.<br />
etc.
Note that $c$ must always belong to $S$, and each player can increase $c$ by at most $n$.

Let $M(n)$ be the highest number that the first player could choose at the start to force a win, and $M(n) = 0$ if there is no such move. For example, $M(2) = 2$, $M(7) = 1$, and $M(20) = 4$.

It can be verified that $\sum{M(n)^3} = 8150$ for $1 \le n \le 20$.

Find $\sum{M(n)^3}$ for $1 \le n \le 1000$.


# Project Euler 391
## 题目
### Hopping Game

Let s_k be the number of 1’s when writing the numbers from 0 to k in binary.<br>For example, writing 0 to 5 in binary, we have 0, 1, 10, 11, 100, 101. There are seven 1’s, so s_5 = 7.<br>The sequence S = {s_k : k \ge 0} starts {0, 1, 2, 4, 5, 7, 9, 12, \dots}.
A game is played by two players. Before the game starts, a number n is chosen. A counter c starts at 0. At each turn, the player chooses a number from 1 to n (inclusive) and increases c by that number. The resulting value of c must be a member of S. If there are no more valid moves, the player loses.
For example:<br>Let n = 5. c starts at 0.<br>Player 1 chooses 4, so c becomes 0 + 4 = 4.<br>Player 2 chooses 5, so c becomes 4 + 5 = 9.<br>Player 1 chooses 3, so c becomes 9 + 3 = 12.<br>etc.<br>Note that c must always belong to S, and each player can increase c by at most n.
Let M(n) be the highest number the first player can choose at her first turn to force a win, and M(n) = 0 if there is no such move. For example, M(2) = 2, M(7) = 1 and M(20) = 4.
Given \sum(M(n))^3 = 8150 for 1 \le n \le 20.
Find \sum(M(n))^3 for 1 \le n \le 1000.


## 解决方案


## 代码


