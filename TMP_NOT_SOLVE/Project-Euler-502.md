---
title: Project Euler 502
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 502
## 题目
### Counting Castles

We define a <i>block</i> to be a rectangle with a height of 1 and an integer-valued length. Let a <i>castle</i> be a configuration of stacked blocks.

Given a game grid that is <var>w</var> units wide and <var>h</var> units tall, a castle is generated according to the following rules:


<ol><li>Blocks can be placed on top of other blocks as long as nothing sticks out past the edges or hangs out over open space.</li>
<li>All blocks are aligned/snapped to the grid.</li>
<li>Any two neighboring blocks on the same row have at least one unit of space between them.</li>
<li>The bottom row is occupied by a block of length <var>w</var>.</li>
<li>The maximum achieved height of the entire castle is exactly <var>h</var>.</li>
<li>The castle is made from an even number of blocks.</li>
</ol>The following is a sample castle for <var>w</var>=8 and <var>h</var>=5:

<p align="center"><img src="project/images/p502_castles.png" alt="p502_castles.png" />

Let F(<var>w</var>,<var>h</var>) represent the number of valid castles, given grid parameters <var>w</var> and <var>h</var>.

For example, F(4,2) = 10, F(13,10) = 3729050610636, F(10,13) = 37959702514, and F(100,100) mod 1 000 000 007 = 841913936.

Find (F(10^12,100) + F(10000,10000) + F(100,10^12)) mod 1 000 000 007.


# Project Euler 502
## 题目
### Counting Castles

We define a <i>block</i> to be a rectangle with a height of 1 and an integer-valued length. Let a <i>castle</i> be a configuration of stacked blocks.
Given a game grid that is w units wide and h units tall, a castle is generated according to the following rules:
<ol>
<li>Blocks can be placed on top of other blocks as long as nothing sticks out past the edges or hangs out over open space.</li>
<li>All blocks are aligned/snapped to the grid.</li>
<li>Any two neighboring blocks on the same row have at least one unit of space between them.</li>
<li>The bottom row is occupied by a block of length w.</li>
<li>The maximum achieved height of the entire castle is exactly h.</li>
<li>The castle is made from an even number of blocks.</li>
</ol>
The following is a sample castle for w=8 and h=5:
<center><img src="https://projecteuler.net/project/images/p502_castles.png"></center>

Let F(w,h) represent the number of valid castles, given grid parameters w and h.
For example, F(4,2) = 10, F(13,10) = 3729050610636, F(10,13) = 37959702514, and F(100,100) mod 1 000 000 007 = 841913936.
Find F(10^12,100) + F(10000,10000) + F(100,10^12) mod 1 000 000 007.


## 解决方案


## 代码


