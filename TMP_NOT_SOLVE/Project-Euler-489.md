---
title: Project Euler 489
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 489
## 题目
### Common factors between two sequences


Let <var>G</var>(<var>a</var>, <var>b</var>) be the smallest non-negative integer <var>n</var> for which <dfn title="Greatest common divisor">gcd</dfn>(<var>n</var>^3 + <var>b</var>, (<var>n</var> + <var>a</var>)^3 + <var>b</var>) is maximized.<br />
For example, <var>G</var>(1, 1) = 5 because gcd(<var>n</var>^3 + 1, (<var>n</var> + 1)^3 + 1) reaches its maximum value of 7 for <var>n</var> = 5, and is smaller for 0 \le n < 5.<br />
Let <var>H</var>(<var>m</var>, <var>n</var>) = <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> <var>G</var>(<var>a</var>, <var>b</var>) for 1 \le <var>a</var> \le <var>m</var>, 1 \le <var>b</var> \le <var>n</var>.<br />
You are given <var>H</var>(5, 5) = 128878 and <var>H</var>(10, 10) = 32936544.
Find <var>H</var>(18, 1900).


# Project Euler 489
## 题目
### Common factors between two sequences

Let G(a, b) be the smallest non-negative integer n for which <dfn title="Greatest common divisor">gcd</dfn>(n^3 + b, (n + a)^3 + b) is maximized.<br>For example, G(1, 1) = 5 because gcd(n^3 + 1, (n + 1)^3 + 1) reaches its maximum value of 7 for n = 5, and is smaller for 0 \le n < 5.<br>Let H(m, n) = \sum G(a, b) for 1 \le a \le m, 1 \le b \le n.<br>You are given H(5, 5) = 128878 and H(10, 10) = 32936544.
Find H(18, 1900).


## 解决方案


## 代码


