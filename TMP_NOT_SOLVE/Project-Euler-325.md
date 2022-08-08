---
title: Project Euler 325
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 325
## 题目
### Stone Game II


A game is played with two piles of stones and two players.<br />
On each player's turn, the player may remove a number of stones from the larger pile.<br />
The number of stones removed must be a positive multiple of the number of stones in the smaller pile.

E.g. Let the ordered pair $(6,14)$ describe a configuration with 6 stones in the smaller pile and 14 stones in the larger pile, then the first player can remove 6 or 12 stones from the larger pile.

The player taking all the stones from a pile wins the game.

A <dfn>winning configuration</dfn> is one where the first player can force a win. For example, $(1,5)$, $(2,6)$, and $(3,12)$ are winning configurations because the first player can immediately remove all stones in the second pile.

A <dfn>losing configuration</dfn> is one where the second player can force a win, no matter what the first player does. For example, $(2,3)$ and $(3,4)$ are losing configurations: any legal move leaves a winning configuration for the second player.

Define $S(N)$ as the sum of $(x_i + y_i)$ for all losing configurations $(x_i, y_i), 0 \lt x_i \lt y_i \le N$.<br />
We can verify that $S(10) = 211$ and $S(10^4) = 230312207313$.

Find $S(10^{16}) \mod 7^{10}$.


# Project Euler 325
## 题目
### Stone Game II

A game is played with two piles of stones and two players. At her turn, a player removes a number of stones from the larger pile. The number of stones she removes must be a positive multiple of the number of stones in the smaller pile.
E.g., let the ordered pair(6,14) describe a configuration with 6 stones in the smaller pile and 14 stones in the larger pile, then the first player can remove 6 or 12 stones from the larger pile.
The player taking all the stones from a pile wins the game.
A <i>winning configuration</i> is one where the first player can force a win. For example, (1,5), (2,6) and (3,12) are winning configurations because the first player can immediately remove all stones in the second pile.
A <i>losing configuration</i> is one where the second player can force a win, no matter what the first player does. For example, (2,3) and (3,4) are losing configurations: any legal move leaves a winning configuration for the second player.
Define S(N) as the sum of (x_i+y_i) for all losing configurations (x_i,y_i), 0 < x_i < y_i \le N. We can verify that S(10) = 211 and S(10^4) = 230312207313.
Find S(10^16) mod 7^10.


## 解决方案


## 代码


