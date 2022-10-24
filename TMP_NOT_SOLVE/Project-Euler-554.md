---
title: Project Euler 554
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 554
## 题目
### Centaurs on a chess board


On a chess board, a centaur moves like a king or a knight. The diagram below shows the valid moves of a centaur (represented by an inverted king) on an 8x8 board.

<div align="center"><img src="project/images/p554-centaurs.png" alt="p554-centaurs.png" /></div>

It can be shown that at most <var>n</var>^2 non-attacking centaurs can be placed on a board of size 2<var>n</var>\times2<var>n</var>.<br />
Let <var>C</var>(<var>n</var>) be the number of ways to place <var>n</var>^2 centaurs on a 2<var>n</var>\times2<var>n</var> board so that no centaur attacks another directly.<br />
For example <var>C</var>(1) = 4, <var>C</var>(2) = 25, <var>C</var>(10) = 1477721.

Let <var>F_i</var> be the <var>i</var>^th Fibonacci number defined as <var>F</var>_1 = <var>F</var>_2 = 1 and <var>F</var>_i = <var>F</var>_<var>i</var>-1 + <var>F</var>_<var>i</var>-2 for <var>i</var> > 2.

Find $\displaystyle \left( \sum_{i=2}^{90} C(F_i) \right) \text{mod } (10^8+7)$.


# Project Euler 554
## 题目
### Centaurs on a chess board

On a chess board, a centaur moves like a king or a knight. The diagram below shows the valid moves of a centaur (represented by an inverted king) on an 8x8 board.
<center><img src="https://projecteuler.net/project/images/p554-centaurs.png" alt="p554-centaurs.png"></center>

It can be shown that at most n^2 non-attacking centaurs can be placed on a board of size 2n\times2n.<br>Let C(n) be the number of ways to place n^2 centaurs on a 2n\times2n board so that no centaur attacks another directly.<br>For example C(1)&nbsp;=&nbsp;4, C(2)&nbsp;=&nbsp;25, C(10)&nbsp;=&nbsp;1477721.
Let F_i be the i^th Fibonacci number defined as F_1&nbsp;=&nbsp;F_2&nbsp;=&nbsp;1 and F_i&nbsp;=&nbsp;F_i-1&nbsp;+&nbsp;F_i-2 for i&nbsp;>&nbsp;2.
Find $\displaystyle \left( \sum_{i=2}^{90} C(F_i) \right) \text{mod } (10^8+7)$.


## 解决方案


## 代码


