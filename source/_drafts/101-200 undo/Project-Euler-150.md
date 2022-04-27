---
title: Project Euler 150
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 150
## 题目
### Searching a triangular array for a sub-triangle having minimum-sum

In a triangular array of positive and negative integers, we wish to find a sub-triangle such that the sum of the numbers it contains is the smallest possible.
In the example below, it can be easily verified that the marked triangle satisfies this condition having a sum of −42.
<div class="center">
<img src="project/images/p150.gif" class="dark_img" alt="" />

# Project Euler 150
## 题目
### Searching a triangular array for a sub-triangle having minimum-sum
In a triangular array of positive and negative integers, we wish to find a sub-triangle such that the sum of the numbers it contains is the smallest possible.
In the example below, it can be easily verified that the marked triangle satisfies this condition having a sum of -42.
<center><img src="https://projecteuler.net/project/images/p150.gif" border="0" alt=""></center>

We wish to make such a triangular array with one thousand rows, so we generate 500500 pseudo-random numbers s_k in the range ±2^19, using a type of random number generator (known as a Linear Congruential Generator) as follows:
t := 0<br>for k = 1 up to k = 500500:<br>&nbsp;&nbsp;t := (615949*t + 797807) modulo 2^20<br>&nbsp;&nbsp;s_k := t-2^19
Thus: s_1 = 273519, s_2 = -153582, s_3 = 450905 etc
Our triangular array is then formed using the pseudo-random numbers thus:
<center>s_1
s_2&nbsp; s_3
s_4&nbsp; s_5&nbsp; s_6&nbsp; 
s_7&nbsp; s_8&nbsp; s_9&nbsp; s_10
\dots</center>

Sub-triangles can start at any element of the array and extend down as far as we like (taking-in the two elements directly below it from the next row, the three elements directly below from the row after that, and so on).<br>The “sum of a sub-triangle” is defined as the sum of all the elements it contains.<br>Find the smallest possible sub-triangle sum.


## 解决方案


## 代码


