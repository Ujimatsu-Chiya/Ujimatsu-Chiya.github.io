---
title: Project Euler 497
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 497
## 题目
### Drunken Tower of Hanoi


Bob is very familiar with the famous mathematical puzzle/game, "Tower of Hanoi," which consists of three upright rods and disks of different sizes that can slide onto any of the rods. The game begins with a stack of <var>n</var> disks placed on the leftmost rod in descending order by size. The objective of the game is to move all of the disks from the leftmost rod to the rightmost rod, given the following restrictions:

<ol><li>Only one disk can be moved at a time.</li>
<li>A valid move consists of taking the top disk from one stack and placing it onto another stack (or an empty rod).</li>
<li>No disk can be placed on top of a smaller disk.</li>
</ol>Moving on to a variant of this game, consider a long room <var>k</var> units (square tiles) wide, labeled from 1 to <var>k</var> in ascending order. Three rods are placed at squares <var>a</var>, <var>b</var>, and <var>c</var>, and a stack of <var>n</var> disks is placed on the rod at square <var>a</var>.

Bob begins the game standing at square <var>b</var>. His objective is to play the Tower of Hanoi game by moving all of the disks to the rod at square <var>c</var>. However, Bob can only pick up or set down a disk if he is on the same square as the rod / stack in question.

Unfortunately, Bob is also drunk. On a given move, Bob will either stumble one square to the left or one square to the right with equal probability, unless Bob is at either end of the room, in which case he can only move in one direction. Despite Bob's inebriated state, he is still capable of following the rules of the game itself, as well as choosing when to pick up or put down a disk.

The following animation depicts a side-view of a sample game for <var>n</var> = 3, <var>k</var> = 7, <var>a</var> = 2, <var>b</var> = 4, and <var>c</var> = 6:

<p align="center"><img src="project/images/p497_hanoi.gif" alt="p497_hanoi.gif" />

Let E(<var>n</var>,<var>k</var>,<var>a</var>,<var>b</var>,<var>c</var>) be the expected number of squares that Bob travels during a single optimally-played game. A game is played optimally if the number of disk-pickups is minimized.

Interestingly enough, the result is always an integer. For example, E(2,5,1,3,5) = 60 and E(3,20,4,9,17) = 2358.

Find the last nine digits of \sum_1\le<var>n</var>\le10000 E(<var>n</var>,10^<var>n</var>,3^<var>n</var>,6^<var>n</var>,9^<var>n</var>).


# Project Euler 497
## 题目
### Drunken Tower of Hanoi

Bob is very familiar with the famous mathematical puzzle/game, “Tower of Hanoi,” which consists of three upright rods and disks of different sizes that can slide onto any of the rods. The game begins with a stack of n disks placed on the leftmost rod in descending order by size. The objective of the game is to move all of the disks from the leftmost rod to the rightmost rod, given the following restrictions:
<ol>
<li>Only one disk can be moved at a time.</li>
<li>A valid move consists of taking the top disk from one stack and placing it onto another stack (or an empty rod).</li>
<li>No disk can be placed on top of a smaller disk.</li>
</ol>
Moving on to a variant of this game, consider a long room k units (square tiles) wide, labeled from 1 to k in ascending order. Three rods are placed at squares a, b, and c, and a stack of n disks is placed on the rod at square a.
Bob begins the game standing at square b. His objective is to play the Tower of Hanoi game by moving all of the disks to the rod at square c. However, Bob can only pick up or set down a disk if he is on the same square as the rod / stack in question.
Unfortunately, Bob is also drunk. On a given move, Bob will either stumble one square to the left or one square to the right with equal probability, unless Bob is at either end of the room, in which case he can only move in one direction. Despite Bob’s inebriated state, he is still capable of following the rules of the game itself, as well as choosing when to pick up or put down a disk.
The following animation depicts a side-view of a sample game for n = 3, k = 7, a = 2, b = 4, and c = 6:
<center><img src="https://projecteuler.net/project/images/p497_hanoi.gif"></center>

Let E(n,k,a,b,c) be the expected number of squares that Bob travels during a single optimally-played game. A game is played optimally if the number of disk-pickups is minimized.
Interestingly enough, the result is always an integer. For example, E(2,5,1,3,5) = 60 and E(3,20,4,9,17) = 2358.
Find the last nine digits of \sum_1\len\le10000 E(n,10^n,3^n,6^n,9^n).


## 解决方案


## 代码


