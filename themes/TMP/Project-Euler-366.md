---
title: Project Euler 366
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 366
## 题目
### Stone Game III


Two players, Anton and Bernhard, are playing the following game.<br />
There is one pile of n stones.<br />
The first player may remove any positive number of stones, but not the whole pile.<br />
Thereafter, each player may remove at most twice the number of stones his opponent took on the previous move.<br />
The player who removes the last stone wins.


E.g. n=5<br />
If the first player takes anything more than one stone the next player will be able to take all remaining stones.<br />
If the first player takes one stone, leaving four, his opponent will take also one stone, leaving three stones.<br />
The first player cannot take all three because he may take at most 2x1=2 stones. So let's say he takes also one stone, leaving 2. The second player can take the two remaining stones and wins.<br />
So 5 is a losing position for the first player.<br />
For some winning positions there is more than one possible move for the first player.<br />
E.g. when n=17 the first player can remove one or four stones.


Let M(n) be the maximum number of stones the first player can take from a winning position <i>at his first turn</i> and M(n)=0 for any other position.


<span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> M(n) for n\le100 is 728.


Find  <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> M(n) for n\le10^18.
Give your answer modulo 10^8.



# Project Euler 366
## 题目
### Stone Game III

Two players, Anton and Bernhard, are playing the following game.<br>There is one pile of n stones.<br>The first player may remove any positive number of stones, but not the whole pile.<br>Thereafter, each player may remove at most twice the number of stones his opponent took on the previous move.<br>The player who removes the last stone wins.
E.g. n=5<br>If the first player takes anything more than one stone the next player will be able to take all remaining stones.<br>If the first player takes one stone, leaving four, his opponent will take also one stone, leaving three stones.<br>The first player cannot take all three because he may take at most 2x1=2 stones. So let’s say he takes also one stone, leaving 2. The second player can take the two remaining stones and wins.<br>So 5 is a losing position for the first player.<br>For some winning positions there is more than one possible move for the first player.<br>E.g. when n=17 the first player can remove one or four stones.
Let M(n) be the maximum number of stones the first player can take from a winning position <i>at his first turn</i> and M(n)=0 for any other position.
\sumM(n) for n\le100 is 728.
Find \sumM(n) for n\le10^18. Give your answer modulo 10^8.


## 解决方案


## 代码


