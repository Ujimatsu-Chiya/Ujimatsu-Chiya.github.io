---
title: Project Euler 289
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 289
## 题目
### Eulerian Cycles

Let C(<var>x</var>,<var>y</var>) be a circle passing through the points (<var>x</var>, <var>y</var>), (<var>x</var>, <var>y</var>+1), (<var>x</var>+1, <var>y</var>) and (<var>x</var>+1, <var>y</var>+1).

For positive integers m and n, let E(<var>m</var>,<var>n</var>) be a configuration which consists of the <var>m</var>·<var>n</var> circles:<br />
{ C(<var>x</var>,<var>y</var>): 0 \le <var>x</var> < <var>m</var>, 0 \le <var>y</var> < <var>n</var>, <var>x</var> and <var>y</var> are integers }

An Eulerian cycle on E(<var>m</var>,<var>n</var>) is a closed path that passes through each arc exactly once.<br />
Many such paths are possible on E(<var>m</var>,<var>n</var>), but we are only interested in those which are not self-crossing: 
A non-crossing path just touches itself at lattice points, but it never crosses itself.

The image below shows E(3,3) and an example of an Eulerian non-crossing path.<br /><div align="center"><img src="project/images/p289_euler.gif" alt="p289_euler.gif" /></div>

Let L(<var>m</var>,<var>n</var>) be the number of Eulerian non-crossing paths on E(<var>m</var>,<var>n</var>).<br />
For example, L(1,2) = 2, L(2,2) = 37 and L(3,3) = 104290.

Find L(6,10) mod 10^10.


# Project Euler 289
## 题目
### Eulerian Cycles

Let C(x,y) be a circle passing through the points (x,&thinsp;y), (x,&thinsp;y+1), (x+1,&thinsp;y) and (x+1,&thinsp;y+1).
For positive integers m and n, let E(m,n) be a configuration which consists of the m·n circles:<br>{ C(x,y): 0&thinsp;\le&thinsp;x&thinsp;<&thinsp;m, 0&thinsp;\le&thinsp;y&thinsp;<&thinsp;n, x and y are integers }
An Eulerian cycle on E(m,n) is a closed path that passes through each arc exactly once.<br>Many such paths are possible on E(m,n), but we are only interested in those which are not self-crossing: A non-crossing path just touches itself at lattice points, but it never crosses itself.
The image below shows E(3,3) and an example of an Eulerian non-crossing path.
<center><img src="https://projecteuler.net/project/images/p289_euler.gif"></center>

Let L(m,n) be the number of Eulerian non-crossing paths on E(m,n).<br>For example, L(1,2)&thinsp;=&thinsp;2, L(2,2)&thinsp;=&thinsp;37 and L(3,3)&thinsp;=&thinsp;104290.
Find L(6,10) mod 10^10.


## 解决方案


## 代码


