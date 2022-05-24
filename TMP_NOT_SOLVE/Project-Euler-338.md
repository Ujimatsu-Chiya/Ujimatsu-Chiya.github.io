---
title: Project Euler 338
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 338
## 题目
### Cutting Rectangular Grid Paper

A rectangular sheet of grid paper with integer dimensions <var>w</var> \times <var>h</var> is given. Its grid spacing is 1.<br />
When we cut the sheet along the grid lines into two pieces and rearrange those pieces without overlap, we can make new rectangles with different dimensions.
For example, from a sheet with dimensions 9 \times 4 , we can make rectangles with dimensions 18 \times 2, 12 \times 3 and 6 \times 6 by cutting and rearranging as below:

<div align="center">
<img src="project/images/p338_gridpaper.gif" alt="p338_gridpaper.gif" /><br /></div>

Similarly, from a sheet with dimensions 9 \times 8 , we can make rectangles with dimensions 18 \times 4 and 12 \times 6 .

For a pair <var>w</var> and <var>h</var>, let F(<var>w</var>,<var>h</var>) be the number of distinct rectangles that can be made from a sheet with dimensions <var>w</var> \times <var>h</var> .<br />
For example, F(2,1) = 0, F(2,2) = 1, F(9,4) = 3 and F(9,8) = 2. <br />
Note that rectangles congruent to the initial one are not counted in F(<var>w</var>,<var>h</var>).<br />
Note also that rectangles with dimensions <var>w</var> \times <var>h</var> and dimensions <var>h</var> \times <var>w</var> are not considered distinct.

For an integer <var>N</var>, let G(<var>N</var>) be the sum of F(<var>w</var>,<var>h</var>) for all pairs <var>w</var> and <var>h</var> which satisfy 0 < <var>h</var> \le <var>w</var> \le <var>N</var>.<br />
We can verify that G(10) = 55, G(10^3) = 971745 and G(10^5) = 9992617687.

Find G(10^12). Give your answer modulo 10^8.


# Project Euler 338
## 题目
### Cutting Rectangular Grid Paper

A rectangular sheet of grid paper with integer dimensions w \times h is given. Its grid spacing is 1.<br>When we cut the sheet along the grid lines into two pieces and rearrange those pieces without overlap, we can make new rectangles with different dimensions.
For example, from a sheet with dimensions 9 \times 4 , we can make rectangles with dimensions 18 \times 2, 12 \times 3 and 6 \times 6 by cutting and rearranging as below:
<center><img src="https://projecteuler.net/project/images/p338_gridpaper.gif"></center>

Similarly, from a sheet with dimensions 9 \times 8 , we can make rectangles with dimensions 18 \times 4 and 12 \times 6 .
For a pair w and h, let F(w,h) be the number of distinct rectangles that can be made from a sheet with dimensions w \times h .<br>For example, F(2,1) = 0, F(2,2) = 1, F(9,4) = 3 and F(9,8) = 2.<br>Note that rectangles congruent to the initial one are not counted in F(w,h).<br>Note also that rectangles with dimensions w \times h and dimensions h \times w are not considered distinct.
For an integer N, let G(N) be the sum of F(w,h) for all pairs w and h which satisfy 0 < h \le w \le N.<br>We can verify that G(10) = 55, G(10^3) = 971745 and G(10^5) = 9992617687.
Find G(10^12). Give your answer modulo 10^8.


## 解决方案


## 代码


