---
title: Project Euler 509
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 509
## 题目
### Divisor Nim


Anton and Bertrand love to play three pile Nim.<br />
However, after a lot of games of Nim they got bored and changed the rules somewhat.<br />
They may only take a number of stones from a pile that is a <dfn title="a proper divisor of n is a divisor of n smaller than n">proper divisor</dfn> of the number of stones present in the pile.<br /> E.g. if a pile at a certain moment contains 24 stones they may take only 1,2,3,4,6,8 or 12 stones from that pile.<br />
So if a pile contains one stone they can't take the last stone from it as 1 isn't a proper divisor of 1.<br />
The first player that can't make a valid move loses the game.<br />
Of course both Anton and Bertrand play optimally.

The triple (<var>a</var>,<var>b</var>,<var>c</var>) indicates the number of stones in the three piles.<br />
Let <var>S</var>(<var>n</var>) be the number of winning positions for the next player for 1 \le <var>a</var>, <var>b</var>, <var>c</var> \le <var>n</var>.<br /><var>S</var>(10) = 692 and <var>S</var>(100) = 735494.

Find <var>S</var>(123456787654321) modulo 1234567890.



# Project Euler 509
## 题目
### Divisor Nim

Anton and Bertrand love to play three pile Nim.<br>However, after a lot of games of Nim they got bored and changed the rules somewhat.<br>They may only take a number of stones from a pile that is a <dfn title="a proper divisor of n is a divisor of n smaller than n">proper divisor</dfn> of the number of stones present in the pile.<br>E.g. if a pile at a certain moment contains 24 stones they may take only 1,2,3,4,6,8 or 12 stones from that pile.<br>So if a pile contains one stone they can’t take the last stone from it as 1 isn’t a proper divisor of 1.<br>The first player that can’t make a valid move loses the game.<br>Of course both Anton and Bertrand play optimally.
The triple (a,b,c) indicates the number of stones in the three piles.<br>Let S(n) be the number of winning positions for the next player for 1 \le a, b, c \le n.<br>S(10) = 692 and S(100) = 735494.<br>Find S(123456787654321) modulo 1234567890.


## 解决方案


## 代码


