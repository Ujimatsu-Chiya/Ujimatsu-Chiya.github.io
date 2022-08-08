---
title: Project Euler 405
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 405
## 题目
### A rectangular tiling



We wish to tile a rectangle whose length is twice its width.<br />
Let <var>T</var>(0) be the tiling consisting of a single rectangle.<br />
For <var>n</var> > 0, let <var>T</var>(<var>n</var>) be obtained from <var>T</var>(<var>n</var>-1) by replacing all tiles in the following manner:


<div align="center">
<img src="project/images/p405_tile1.png" alt="p405_tile1.png" /></div>


The following animation demonstrates the tilings <var>T</var>(<var>n</var>) for <var>n</var> from 0 to 5:


<div align="center">
<img src="project/images/p405_tile2.gif" alt="p405_tile2.gif" /></div>


Let <var>f</var>(<var>n</var>) be the number of points where four tiles meet in <var>T</var>(<var>n</var>).<br />
For example, <var>f</var>(1) = 0, <var>f</var>(4) = 82 and <var>f</var>(10^9) mod 17^7 = 126897180.



Find <var>f</var>(10^<var>k</var>) for <var>k</var> = 10^18, give your answer modulo 17^7.



# Project Euler 405
## 题目
### A rectangular tiling

We wish to tile a rectangle whose length is twice its width.<br>Let T(0) be the tiling consisting of a single rectangle.<br>For n > 0, let T(n) be obtained from T(n-1) by replacing all tiles in the following manner:
<center><img src="https://projecteuler.net/project/images/p405_tile1.png"></center>

The following animation demonstrates the tilings T(n) for n from 0 to 5:
<center><img src="https://projecteuler.net/project/images/p405_tile2.gif"></center>

Let f(n) be the number of points where four tiles meet in T(n).<br>For example, f(1) = 0, f(4) = 82 and f(10^9) mod 17^7 = 126897180.
Find f(10^k) for k = 10^18, give your answer modulo 17^7.


## 解决方案


## 代码


