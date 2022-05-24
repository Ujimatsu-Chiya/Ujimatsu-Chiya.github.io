---
title: Project Euler 306
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 306
## 题目
### Paper-strip Game

The following game is a classic example of Combinatorial Game Theory:

Two players start with a strip of $n$ white squares and they take alternate turns.<br />
On each turn, a player picks two contiguous white squares and paints them black.<br />
The first player who cannot make a move loses.

<ul><li>$n = 1$: No valid moves, so the first player loses automatically.</li>
<li>$n = 2$: Only one valid move, after which the second player loses.</li>
<li>$n = 3$: Two valid moves, but both leave a situation where the second player loses.</li>
<li>$n = 4$: Three valid moves for the first player, who is able to win the game by painting the two middle squares.</li>
<li>$n = 5$: Four valid moves for the first player (shown below in red), but no matter what the player does, the second player (blue) wins.</li>
</ul><div class="center"><img src="project/images/p306_pstrip.gif" class="dark_img" alt="p306_pstrip.gif" /></div>

So, for $1 \le n \le 5$, there are 3 values of $n$ for which the first player can force a win.<br />
Similarly, for $1 \le n \le 50$, there are 40 values of $n$ for which the first player can force a win.

For $1 \le n \le 1 000 000$, how many values of $n$ are there for which the first player can force a win?


# Project Euler 306
## 题目
### Paper-strip Game

The following game is a classic example of Combinatorial Game Theory:
Two players start with a strip of n white squares and they take alternate turns.<br>On each turn, a player picks two contiguous white squares and paints them black.<br>The first player who cannot make a move loses.
<ul>
<li>If n = 1, there are no valid moves, so the first player loses automatically.</li>
<li>If n = 2, there is only one valid move, after which the second player loses.</li>
<li>If n = 3, there are two valid moves, but both leave a situation where the second player loses.</li>
<li>If n = 4, there are three valid moves for the first player; she can win the game by painting the two middle squares.</li>
<li>If n = 5, there are four valid moves for the first player (shown below in red); but no matter what she does, the second player (blue) wins.</li>
</ul>
<center><img src="https://projecteuler.net/project/images/p306_pstrip.gif"></center>

So, for 1 \le n \le 5, there are 3 values of n for which the first player can force a win.<br>Similarly, for 1 \le n \le 50, there are 40 values of n for which the first player can force a win.
For 1 \le n \le 1 000 000, how many values of n are there for which the first player can force a win?


## 解决方案


## 代码


