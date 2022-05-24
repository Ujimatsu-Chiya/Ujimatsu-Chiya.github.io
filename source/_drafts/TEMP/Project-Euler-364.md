---
title: Project Euler 364
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 364
## 题目
### Comfortable distance


There are <var>N</var> seats in a row. <var>N</var> people come after each other to fill the seats according to the following rules:
<ol type="1"><li>If there is any seat whose adjacent seat(s) are not occupied take such a seat.</li>
<li>If there is no such seat and there is any seat for which only one adjacent seat is occupied take such a seat.</li>
<li>Otherwise take one of the remaining available seats. </li>
</ol>
Let T(<var>N</var>) be the number of possibilities that <var>N</var> seats are occupied by <var>N</var> people with the given rules.<br /> The following figure shows T(4)=8.


<div align="center">
<img src="project/images/p364_comf_dist.gif" class="dark_img" alt="p364_comf_dist.gif" /></div>

We can verify that T(10) = 61632 and T(1 000) mod 100 000 007 = 47255094.
Find T(1 000 000) mod 100 000 007.


# Project Euler 364
## 题目
### Comfortable distance

There are N seats in a row. N people come after each other to fill the seats according to the following rules:
<ol>
<li>If there is any seat whose adjacent seat(s) are not occupied take such a seat.</li>
<li>If there is no such seat and there is any seat for which only one adjacent seat is occupied take such a seat.</li>
<li>Otherwise take one of the remaining available seats. </li>
</ol>
Let T(N) be the number of possibilities that N seats are occupied by N people with the given rules. The following figure shows T(4)=8.
<center><img src="https://projecteuler.net/project/images/p364_comf_dist.gif"></center>

We can verify that T(10) = 61632 and T(1 000) mod 100 000 007 = 47255094.
Find T(1 000 000) mod 100 000 007.


## 解决方案


## 代码


