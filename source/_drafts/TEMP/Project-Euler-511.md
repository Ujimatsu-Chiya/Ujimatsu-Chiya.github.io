---
title: Project Euler 511
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 511
## 题目
### Sequences with nice divisibility properties

Let <var>Seq</var>(<var>n</var>,<var>k</var>) be the number of positive-integer sequences {<var>a_i</var>}_1\lei\le<var>n</var> of length <var>n</var> such that:
<ul style="list-style-type:disc;"><li><var>n</var> is divisible by <var>a_i</var> for 1 \le <var>i</var> \le <var>n</var>, and</li>
  <li><var>n</var> + <var>a</var>_1 + <var>a</var>_2 + \dots + <var>a_n</var> is divisible by <var>k</var>.</li>
</ul>Examples:
<var>Seq</var>(3,4) = 4, and the 4 sequences are:<br />
{1, 1, 3}<br />
{1, 3, 1}<br />
{3, 1, 1}<br />
{3, 3, 3}
<var>Seq</var>(4,11) = 8, and the 8 sequences are:<br />
{1, 1, 1, 4}<br />
{1, 1, 4, 1}<br />
{1, 4, 1, 1}<br />
{4, 1, 1, 1}<br />
{2, 2, 2, 1}<br />
{2, 2, 1, 2}<br />
{2, 1, 2, 2}<br />
{1, 2, 2, 2}
The last nine digits of <var>Seq</var>(1111,24) are 840643584.
Find the last nine digits of <var>Seq</var>(1234567898765,4321).


# Project Euler 511
## 题目
### Sequences with nice divisibility properties

Let Seq(n,k) be the number of positive-integer sequences {a_i}_1\lei\len of length n such that:
<ul>
<li>n is divisible by a_i for 1&nbsp;\le&nbsp;i&nbsp;\le&nbsp;n, and</li>
<li>n + a_1 + a_2 + \dots + a_n is divisible by k.</li>
</ul>
Examples:
Seq(3,4) = 4, and the 4 sequences are:<br>{1, 1, 3}<br>{1, 3, 1}<br>{3, 1, 1}<br>{3, 3, 3}
Seq(4,11) = 8, and the 8 sequences are:<br>{1, 1, 1, 4}<br>{1, 1, 4, 1}<br>{1, 4, 1, 1}<br>{4, 1, 1, 1}<br>{2, 2, 2, 1}<br>{2, 2, 1, 2}<br>{2, 1, 2, 2}<br>{1, 2, 2, 2}
The last nine digits of Seq(1111,24) are 840643584.
Find the last nine digits of Seq(1234567898765,4321).


## 解决方案


## 代码


