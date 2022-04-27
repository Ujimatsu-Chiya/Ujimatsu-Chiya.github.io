---
title: Project Euler 127
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 127
## 题目
### abc-hits

The radical of <i>n</i>, rad(<i>n</i>), is the product of distinct prime factors of <i>n</i>. For example, 504 = 2^3 × 3^2 × 7, so rad(504) = 2 × 3 × 7 = 42.
We shall define the triplet of positive integers (<i>a</i>, <i>b</i>, <i>c</i>) to be an abc-hit if:
<ol><li>GCD(<i>a,</i> <i>b</i>) = GCD(<i>a</i>, <i>c</i>) = GCD(<i>b</i>, <i>c</i>) = 1</li>
<li><i>a</i> &lt; <i>b</i></li>
<li><i>a</i> + <i>b</i> = <i>c</i></li>
<li>rad(<i>abc</i>) &lt; <i>c</i></li>
</ol>For example, (5, 27, 32) is an abc-hit, because:
<ol><li>GCD(5, 27) = GCD(5, 32) = GCD(27, 32) = 1</li>
<li>5 &lt; 27</li>
<li>5 + 27 = 32</li>
<li>rad(4320) = 30 &lt; 32</li>
</ol>It turns out that abc-hits are quite rare and there are only thirty-one abc-hits for <i>c</i> &lt; 1000, with ∑<i>c</i> = 12523.
Find ∑<i>c</i> for <i>c</i> &lt; 120000.



# Project Euler 127
## 题目
### abc-hits
The radical of n, rad(n), is the product of distinct prime factors of n. For example, 504 = 2^3 × 3^2 × 7, so rad(504) = 2 × 3 × 7 = 42.
We shall define the triplet of positive integers (a, b, c) to be an abc-hit if:
<ol>
<li>GCD(a, b) = GCD(a, c) = GCD(b, c) = 1</li>
<li>a &lt; b</li>
<li>a + b = c</li>
<li>rad(abc) &lt; c</li>
</ol>
For example, (5, 27, 32) is an abc-hit, because:
<ol>
<li>GCD(5, 27) = GCD(5, 32) = GCD(27, 32) = 1</li>
<li>5 &lt; 27</li>
<li>5 + 27 = 32</li>
<li>rad(4320) = 30 &lt; 32</li>
</ol>
It turns out that abc-hits are quite rare and there are only thirty-one abc-hits for c &lt; 1000, with ∑c = 12523.
Find ∑c for c &lt; 120000.


## 解决方案


## 代码


