---
title: Project Euler 508
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 508
## 题目
### Integers in base i-1


Consider the Gaussian integer i-1. A <b>base i-1 representation</b> of a Gaussian integer <var>a</var>+<var>b</var>i is a finite sequence of digits <var>d</var>_<var>n</var>-1<var>d</var>_<var>n</var>-2\dots<var>d</var>_1<var>d</var>_0 such that:

<ul><li><var>a</var>+<var>b</var>i = <var>d</var>_<var>n</var>-1(i-1)^<var>n</var>-1 + <var>d</var>_<var>n</var>-2(i-1)^<var>n</var>-2 + \dots + <var>d</var>_1(i-1) + <var>d</var>_0</li>
<li>Each <var>d</var>_<var>k</var> is in {0,1}</li>
<li>There are no leading zeroes, i.e. <var>d</var>_n-1 ≠ 0, unless <var>a</var>+<var>b</var>i is itself 0</li>
</ul>Here are base i-1 representations of a few Gaussian integers:<br /><br />
11+24i → 111010110001101<br />
24-11i → 110010110011<br />
8+0i → 111000000<br />
-5+0i → 11001101<br />
0+0i → 0

Remarkably, every Gaussian integer has a unique base i-1 representation!<br /><br />

Define <var>f</var>(<var>a</var>+<var>b</var>i) as the number of 1s in the unique base i-1 representation of <var>a</var>+<var>b</var>i. For example, <var>f</var>(11+24i) = 9 and <var>f</var>(24-11i) = 7.<br /><br />

Define <var>B</var>(<var>L</var>) as the sum of <var>f</var>(<var>a</var>+<var>b</var>i) for all integers <var>a</var>, <var>b</var> such that |<var>a</var>| \le <var>L</var> and |<var>b</var>| \le <var>L</var>. For example, <var>B</var>(500) = 10795060.<br /><br />

Find <var>B</var>(10^15) mod 1 000 000 007.


# Project Euler 508
## 题目
### Integers in base i-1

Consider the Gaussian integer i-1. A **base i-1 representation** of a Gaussian integer a+bi is a finite sequence of digits d_n-1d_n-2\dotsd_1d_0 such that:
<ul>
<li>a+bi = d_n-1(i-1)^n-1 + d_n-2(i-1)^n-2 + \dots + d_1(i-1) + d_0</li>
<li>Each d_k is in {0,1}</li>
<li>There are no leading zeroes, i.e. d_n-1 ≠ 0, unless a+bi is itself 0</li>
</ul>
Here are base i-1 representations of a few Gaussian integers:
11+24i → 111010110001101<br>24-11i → 110010110011<br>8+0i → 111000000<br>-5+0i → 11001101<br>0+0i → 0
Remarkably, every Gaussian integer has a unique base i-1 representation!
Define f(a+bi) as the number of 1s in the unique base i-1 representation of a+bi. For example, f(11+24i) = 9 and f(24-11i) = 7.
Define B(L) as the sum of f(a+bi) for all integers a, b such that |a| \le L and |b| \le L. For example, B(500) = 10795060.
Find B(10^15) mod 1 000 000 007.


## 解决方案


## 代码


