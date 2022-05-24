---
title: Project Euler 262
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 262
## 题目
### Mountain Range

The following equation represents the <i>continuous</i> topography of a mountainous region, giving the <dfn title="height above sea level">elevation</dfn> <var>h</var> at any point (<var>x</var>,<var>y</var>):

<div align="center">
<img src="project/images/p262_formula1.gif" class="dark_img" alt="p262_formula1.gif" /><br /></div>

A mosquito intends to fly from A(200,200) to B(1400,1400), without leaving the area given by 0 \le <var>x</var>, <var>y</var> \le 1600.

Because of the intervening mountains, it first rises straight up to a point A', having elevation <var>f</var>. Then, while remaining at the same elevation <var>f</var>, it flies around any obstacles until it arrives at a point B' directly above B.

First, determine <var>f_min</var> which is the minimum constant elevation allowing such a trip from A to B, while remaining in the specified area.<br />
Then, find the length of the shortest path between A' and B', while flying at that constant elevation <var>f_min</var>.

Give that length as your answer, rounded to three decimal places.

<font><u>Note</u>: For convenience, the elevation function shown above is repeated below, in a form suitable for most programming languages:<br />
h=( 5000-0.005*(x*x+y*y+x*y)+12.5*(x+y) ) * exp( -abs(0.000001*(x*x+y*y)-0.0015*(x+y)+0.7) )</font>



# Project Euler 262
## 题目
### Mountain Range

The following equation represents the <em>continuous</em> topography of a mountainous region, giving the <dfn title="height above sea level">elevation</dfn> h at any point (x,y):
<center><img src="https://projecteuler.net/project/images/p262_formula1.gif"></center>

A mosquito intends to fly from A(200,200) to B(1400,1400), without leaving the area given by 0&nbsp;\le&nbsp;x,&nbsp;y&nbsp;\le&nbsp;1600.
Because of the intervening mountains, it first rises straight up to a point A’, having elevation f. Then, while remaining at the same elevation f, it flies around any obstacles until it arrives at a point B’ directly above B.
First, determine f_min which is the minimum constant elevation allowing such a trip from A to B, while remaining in the specified area.<br>Then, find the length of the shortest path between A’ and B’, while flying at that constant elevation f_min.
Give that length as your answer, rounded to three decimal places.
<u>Note</u>: For convenience, the elevation function shown above is repeated below, in a form suitable for most programming languages:<br>h=(5000-0.005*(x*x+y*y+x*y)+12.5*(x+y))*exp(-abs(0.000001*(x*x+y*y)-0.0015*(x+y)+0.7))


## 解决方案


## 代码


