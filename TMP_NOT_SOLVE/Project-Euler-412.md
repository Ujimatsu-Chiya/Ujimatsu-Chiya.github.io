---
title: Project Euler 412
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 412
## 题目
### Gnomon numbering


For integers <var>m</var>, <var>n</var> (0 \le <var>n</var> < <var>m</var>), let L(<var>m</var>, <var>n</var>) be an <var>m</var>\times<var>m</var> grid with the top-right <var>n</var>\times<var>n</var> grid removed.

For example, L(5, 3) looks like this:

<p class="center"><img src="project/images/p412_table53.png" alt="p412_table53.png" />

We want to number each cell of L(<var>m</var>, <var>n</var>) with consecutive integers 1, 2, 3, \dots such that the number in every cell is smaller than the number below it and to the left of it.

For example, here are two valid numberings of L(5, 3):
<p class="center"><img src="project/images/p412_tablenums.png" alt="p412_tablenums.png" />

Let LC(<var>m</var>, <var>n</var>) be the number of valid numberings of L(<var>m</var>, <var>n</var>).<br />
It can be verified that LC(3, 0) = 42, LC(5, 3) = 250250, LC(6, 3) = 406029023400 and LC(10, 5) mod 76543217 = 61251715.

Find LC(10000, 5000) mod 76543217.


# Project Euler 412
## 题目
### Gnomon numbering

For integers m, n (0&nbsp;\le&nbsp;n&nbsp;<&nbsp;m), let L(m,&nbsp;n) be an m\timesm grid with the top-right n\timesn grid removed.
For example, L(5, 3) looks like this:
<center><img src="https://projecteuler.net/project/images/p412_table53.png"></center>

We want to number each cell of L(m,&nbsp;n) with consecutive integers 1, 2, 3, \dots such that the number in every cell is smaller than the number below it and to the left of it.
For example, here are two valid numberings of L(5,&nbsp;3):
<center><img src="https://projecteuler.net/project/images/p412_tablenums.png"></center>

Let LC(m, n) be the number of valid numberings of L(m, n).<br>It can be verified that LC(3,&nbsp;0) = 42, LC(5,&nbsp;3) = 250250, LC(6,&nbsp;3) = 406029023400 and LC(10,&nbsp;5) mod 76543217 = 61251715.
Find LC(10000,&nbsp;5000) mod 76543217.


## 解决方案


## 代码


