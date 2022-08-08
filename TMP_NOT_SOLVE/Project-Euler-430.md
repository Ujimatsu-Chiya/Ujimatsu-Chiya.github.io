---
title: Project Euler 430
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 430
## 题目
### Range flips


<var>N</var> disks are placed in a row, indexed 1 to <var>N</var> from left to right.<br />
Each disk has a black side and white side. Initially all disks show their white side.

At each turn, two, not necessarily distinct, integers <var>A</var> and <var>B</var> between 1 and <var>N</var> (inclusive) are chosen uniformly at random.<br />
All disks with an index from <var>A</var> to <var>B</var> (inclusive) are flipped.

The following example shows the case <var>N</var> = 8. At the first turn <var>A</var> = 5 and <var>B</var> = 2, and at the second turn <var>A</var> = 4 and <var>B</var> = 6.

<p align="center"><img src="project/images/p430_flips.gif" class="dark_img" alt="p430_flips.gif" />

Let E(<var>N</var>, <var>M</var>) be the expected number of disks that show their white side after <var>M</var> turns.<br />
We can verify that E(3, 1) = 10/9, E(3, 2) = 5/3, E(10, 4) ≈ 5.157 and E(100, 10) ≈ 51.893.

Find E(10^10, 4000).<br />
Give your answer rounded to 2 decimal places behind the decimal point.


# Project Euler 430
## 题目
### Range flips

N disks are placed in a row, indexed 1 to N from left to right.<br>Each disk has a black side and white side. Initially all disks show their white side.
At each turn, two, not necessarily distinct, integers A and B between 1 and N (inclusive) are chosen uniformly at random.<br>All disks with an index from A to B (inclusive) are flipped.
The following example shows the case N = 8. At the first turn A = 5 and B = 2, and at the second turn A = 4 and B = 6.
<center><img src="https://projecteuler.net/project/images/p430_flips.gif"></center>

Let E(N, M) be the expected number of disks that show their white side after M turns.<br>We can verify that E(3, 1) = 10/9, E(3, 2) = 5/3, E(10, 4) ≈ 5.157 and E(100, 10) ≈ 51.893.
Find E(10^10, 4000).<br>Give your answer rounded to 2 decimal places behind the decimal point.


## 解决方案


## 代码


