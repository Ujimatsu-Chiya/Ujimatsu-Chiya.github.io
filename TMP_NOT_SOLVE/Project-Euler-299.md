---
title: Project Euler 299
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 299
## 题目
### Three similar triangles


Four points with integer coordinates are selected:<br />A(<var>a</var>, 0), B(<var>b</var>, 0), C(0, <var>c</var>) and D(0, <var>d</var>), 
with 0 < <var>a</var> < <var>b</var> and 0 < <var>c</var> < <var>d</var>.<br />
Point P, also with integer coordinates, is chosen on the line AC so that the three triangles ABP, CDP and BDP are all <dfn title="Have equal angles">similar</dfn>.
<div align="center"><img src="project/images/p299_ThreeSimTri.gif" class="dark_img" alt="p299_ThreeSimTri.gif" /></div>
It is easy to prove that the three triangles can be similar, only if <var>a</var>=<var>c</var>.

So, given that <var>a</var>=<var>c</var>, we are looking for triplets (<var>a</var>,<var>b</var>,<var>d</var>) such that at least one point P (with integer coordinates) exists on AC, making the three triangles ABP, CDP and BDP all similar.

For example, if (<var>a</var>,<var>b</var>,<var>d</var>)=(2,3,4), it can be easily verified that point P(1,1) satisfies the above condition. 
Note that the triplets (2,3,4) and (2,4,3) are considered as distinct, although point P(1,1) is common for both.

If <var>b</var>+<var>d</var> < 100, there are 92 distinct triplets (<var>a</var>,<var>b</var>,<var>d</var>) such that point P exists.<br />
If <var>b</var>+<var>d</var> < 100 000, there are 320471 distinct triplets (<var>a</var>,<var>b</var>,<var>d</var>) such that point P exists.
If <var>b</var>+<var>d</var> < 100 000 000, how many distinct triplets (<var>a</var>,<var>b</var>,<var>d</var>) are there such that point P exists?


# Project Euler 299
## 题目
### Three similar triangles

Four points with integer coordinates are selected:A(a,&nbsp;0), B(b,&nbsp;0), C(0,&nbsp;c) and D(0,&nbsp;d), with 0&nbsp;<&nbsp;a&nbsp;<&nbsp;b and 0&nbsp;<&nbsp;c&nbsp;<&nbsp;d.<br>Point P, also with integer coordinates, is chosen on the line AC so that the three triangles ABP, CDP and BDP are all <dfn title="Have equal angles">similar</dfn>.
<center><img src="https://projecteuler.net/project/images/p299_ThreeSimTri.gif"></center>

It is easy to prove that the three triangles can be similar, only if a=c.
So, given that a=c, we are looking for triplets (a,b,d) such that at least one point P (with integer coordinates) exists on AC, making the three triangles ABP, CDP and BDP all similar.
For example, if (a,b,d)=(2,3,4), it can be easily verified that point P(1,1) satisfies the above condition. Note that the triplets (2,3,4) and (2,4,3) are considered as distinct, although point P(1,1) is common for both.
If b+d&nbsp;<&nbsp;100, there are 92 distinct triplets (a,b,d) such that point P exists.<br>If b+d&nbsp;<&nbsp;100 000, there are 320471 distinct triplets (a,b,d) such that point P exists.
If b+d&nbsp;<&nbsp;100 000 000, how many distinct triplets (a,b,d) are there such that point P exists?


## 解决方案


## 代码


