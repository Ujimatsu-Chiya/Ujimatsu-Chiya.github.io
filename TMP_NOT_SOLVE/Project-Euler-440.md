---
title: Project Euler 440
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 440
## 题目
### GCD and Tiling

We want to tile a board of length <var>n</var> and height 1 completely, with either 1 \times 2 blocks or 1 \times 1 blocks with a single decimal digit on top:
<div class="center">
<img src="project/images/p440_tiles.png" alt="p440_tiles.png" /></div>
For example, here are some of the ways to tile a board of length <var>n</var> = 8:

<div class="center">
<img src="project/images/p440_some8.png" alt="p440_some8.png" /></div>
Let T(<var>n</var>) be the number of ways to tile a board of length <var>n</var> as described above.

For example, T(1) = 10 and T(2) = 101.

Let S(<var>L</var>) be the triple sum <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span>_<var>a</var>,<var>b</var>,<var>c</var> gcd(T(<var>c</var>^<var>a</var>), T(<var>c</var>^<var>b</var>)) for 1 \le <var>a</var>, <var>b</var>, <var>c</var> \le <var>L</var>.<br />
For example:<br />
S(2) = 10444<br />
S(3) = 1292115238446807016106539989<br />
S(4) mod 987 898 789 = 670616280.

Find S(2000) mod 987 898 789.


# Project Euler 440
## 题目
### GCD and Tiling

We want to tile a board of length n and height 1 completely, with either 1 \times 2 blocks or 1 \times 1 blocks with a single decimal digit on top:
<center><img src="https://projecteuler.net/project/images/p440_tiles.png"></center>

For example, here are some of the ways to tile a board of length n = 8:
<center><img src="https://projecteuler.net/project/images/p440_some8.png"></center>

Let T(n) be the number of ways to tile a board of length n as described above.
For example, T(1) = 10 and T(2) = 101.
Let S(L) be the triple sum \sum_a,b,c gcd(T(c^a), T(c^b)) for 1 \le a, b, c \le L.<br>For example:<br>S(2) = 10444<br>S(3) = 1292115238446807016106539989<br>S(4) mod 987&nbsp;898&nbsp;789 = 670616280.
Find S(2000) mod 987&nbsp;898&nbsp;789.


## 解决方案


## 代码


