---
title: Project Euler 312
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 312
## 题目
### Cyclic paths on Sierpiński graphs

- A <b>Sierpiński graph</b> of order-1 (<var>S</var>_1) is an equilateral triangle.<br />
- <var>S</var>_<var>n</var>+1 is obtained from <var>S</var>_<var>n</var> by positioning three copies of <var>S</var>_<var>n</var> so that every pair of copies has one common corner.


<div align="center"><img src="project/images/p312_sierpinskyAt.gif" class="dark_img" alt="p312_sierpinskyAt.gif" /></div>

Let C(<var>n</var>) be the number of cycles that pass exactly once through all the vertices of <var>S</var>_<var>n</var>.<br />
For example, C(3) = 8 because eight such cycles can be drawn on <var>S</var>_3, as shown below:


<div align="center"><img src="project/images/p312_sierpinsky8t.gif" class="dark_img" alt="p312_sierpinsky8t.gif" /></div>

It can also be verified that :<br />
C(1) = C(2) = 1<br />
C(5) = 71328803586048<br />
C(10 000) mod 10^8 = 37652224<br />
C(10 000) mod 13^8 = 617720485<br />

Find C(C(C(10 000))) mod 13^8.





# Project Euler 312
## 题目
### Cyclic paths on Sierpiński graphs

A **Sierpiński graph** of order-1 (S_1) is an equilateral triangle.<br>S_n+1 is obtained from S_n by positioning three copies of S_n so that every pair of copies has one common corner.
<center><img src="https://projecteuler.net/project/images/p312_sierpinskyAt.gif"></center>

Let C(n) be the number of cycles that pass exactly once through all the vertices of S_n.<br>For example, C(3) = 8 because eight such cycles can be drawn on S_3, as shown below:
<center><img src="https://projecteuler.net/project/images/p312_sierpinsky8t.gif"></center>

It can also be verified that :<br>C(1) = C(2) = 1<br>C(5) = 71328803586048<br>C(10 000) mod 10^8 = 37652224<br>C(10 000) mod 13^8 = 617720485
Find C(C(C(10 000))) mod 13^8.


## 解决方案


## 代码


