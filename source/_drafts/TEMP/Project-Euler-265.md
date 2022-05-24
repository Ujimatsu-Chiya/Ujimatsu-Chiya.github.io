---
title: Project Euler 265
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 265
## 题目
### Binary Circles

2^N binary digits can be placed in a circle so that all the N-digit clockwise subsequences are distinct.

For N=3, two such circular arrangements are possible, ignoring rotations:
<div align="center"><img src="project/images/p265_BinaryCircles.gif" class="dark_img" alt="p265_BinaryCircles.gif" /></div>

For the first arrangement, the 3-digit subsequences, in clockwise order, are:<br /> 000, 001, 010, 101, 011, 111, 110 and 100.

Each circular arrangement can be encoded as a number by concatenating the binary digits starting with the subsequence of all zeros as the most significant bits and proceeding clockwise. The two arrangements for N=3 are thus represented as 23 and 29:
<div align="center">00010111 _2 = 23</div>
<div align="center">00011101 _2 = 29</div>

Calling S(N) the sum of the unique numeric representations, we can see that S(3) = 23 + 29 = 52.

Find S(5).



# Project Euler 265
## 题目
### Binary Circles

2^N binary digits can be placed in a circle so that all the N-digit clockwise subsequences are distinct.
For N=3, two such circular arrangements are possible, ignoring rotations:
<center><img src="https://projecteuler.net/project/images/p265_BinaryCircles.gif"></center>

For the first arrangement, the 3-digit subsequences, in clockwise order, are: 000, 001, 010, 101, 011, 111, 110 and 100.
Each circular arrangement can be encoded as a number by concatenating the binary digits starting with the subsequence of all zeros as the most significant bits and proceeding clockwise. The two arrangements for N=3 are thus represented as 23 and 29:
<center>00010111&thinsp;_2 = 23
00011101&thinsp;_2 = 29</center>

Calling S(N) the sum of the unique numeric representations, we can see that S(3) = 23 + 29 = 52.
Find S(5).


## 解决方案


## 代码


