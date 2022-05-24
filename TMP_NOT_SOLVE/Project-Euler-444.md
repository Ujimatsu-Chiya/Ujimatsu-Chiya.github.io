---
title: Project Euler 444
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 444
## 题目
### The Roundtable Lottery

A group of $p$ people decide to sit down at a round table and play a lottery-ticket trading game. Each person starts off with a randomly-assigned, unscratched lottery ticket. Each ticket, when scratched, reveals a whole-pound prize ranging anywhere from £1 to £$p$, with no two tickets alike. The goal of the game is for all of the players to maximize the winnings of the ticket they hold upon leaving the game.

An arbitrary person is chosen to be the first player. Going around the table, each player has only one of two options:

<ol><li>The player can choose to scratch the ticket and reveal its worth to everyone at the table.</li>
<li>If the player's ticket is unscratched, then the player may trade it with a previous player's scratched ticket, and then leaves the game with that ticket. The previous player then scratches the newly-acquired ticket and reveals its worth to everyone at the table.</li>
</ol>The game ends once all tickets have been scratched. All players still remaining at the table must leave with their currently-held tickets.

Assume that players will use the optimal strategy for maximizing the expected value of their ticket winnings.

Let $E(p)$ represent the expected number of players left at the table when the game ends in a game consisting of $p$ players.<br />
E.g. $E(111) = 5.2912$ when rounded to 5 significant digits.

Let $S_1(N) = \sum \limits_{p = 1}^{N} {E(p)}$.<br />
Let $S_k(N) = \sum \limits_{p = 1}^{N} {S_{k-1}(p)}$ for $k \gt 1$.

Find $S_{20}(10^{14})$ and write the answer in scientific notation rounded to 10 significant digits. Use a lowercase e to separate mantissa and exponent. For example, the answer for $S_3(100)$ would be 5.983679014e5.


# Project Euler 444
## 题目
### The Roundtable Lottery

A group of p people decide to sit down at a round table and play a lottery-ticket trading game. Each person starts off with a randomly-assigned, unscratched lottery ticket. Each ticket, when scratched, reveals a whole-pound prize ranging anywhere from £1 to £p, with no two tickets alike. The goal of the game is for each person to maximize his ticket winnings upon leaving the game.
An arbitrary person is chosen to be the first player. Going around the table, each player has only one of two options:
<ol>
<li>The player can scratch his ticket and reveal its worth to everyone at the table.</li>
<li>The player can trade his unscratched ticket for a previous player’s scratched ticket, and then leave the game with that ticket. The previous player then scratches his newly-acquired ticket and reveals its worth to everyone at the table.</li>
</ol>
The game ends once all tickets have been scratched. All players still remaining at the table must leave with their currently-held tickets.
Assume that each player uses the optimal strategy for maximizing the expected value of his ticket winnings. 
Let E(p) represent the expected number of players left at the table when the game ends in a game consisting of p players (e.g. E(111)&nbsp;=&nbsp;5.2912 when rounded to 5 significant digits).
Let S_1(N) = <img style="vertical-align:middle" src="https://projecteuler.net/project/images/p444_sum.png"> E(p)<br>Let S_k(N) = <img style="vertical-align:middle" src="https://projecteuler.net/project/images/p444_sum.png"> S_k-1(p) for k > 1
Find S_20(10^14) and write the answer in scientific notation rounded to 10 significant digits. Use a lowercase e to separate mantissa and exponent (e.g. S_3(100) = 5.983679014e5).


## 解决方案


## 代码


