---
title: Project Euler 515
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 515
## 题目
### Dissonant Numbers

Let <var>d</var>(<var>p</var>,<var>n</var>,0) be the multiplicative inverse of <var>n</var> modulo prime <var>p</var>, defined as <var>n</var> \times <var>d</var>(<var>p</var>,<var>n</var>,0) = 1 mod <var>p</var>.<br />
Let <var>d</var>(<var>p</var>,<var>n</var>,<var>k</var>) = $\sum_{i=1}^n$<var>d</var>(<var>p</var>,<var>i</var>,<var>k</var>−1) for <var>k</var> \ge 1.<br />
Let <var>D</var>(<var>a</var>,<var>b</var>,<var>k</var>) = $\sum$(<var>d</var>(<var>p</var>,<var>p</var>-1,<var>k</var>) mod <var>p</var>) for all primes <var>a</var> \le <var>p</var> < <var>a</var> + <var>b</var>.
You are given:
<ul><li><var>D</var>(101,1,10) = 45</li>
<li><var>D</var>(10^3,10^2,10^2) = 8334</li>
<li><var>D</var>(10^6,10^3,10^3) = 38162302</li></ul>Find <var>D</var>(10^9,10^5,10^5).


# Project Euler 515
## 题目
### Dissonant Numbers

Let d(p,n,0) be the multiplicative inverse of n modulo prime p, defined as n \times d(p,n,0) = 1 mod p.
Let d(p,n,k) = $\Sigma^n_{i=1}$d(p,i,k?1) for k \ge 1.
Let D(a,b,k) = $\Sigma$(d(p,p-1,k) mod p) for all primes a \le p < a + b.
You are given:
<ul>
<li>D(101,1,10) = 45</li>
<li>D(10^3,10^2,10^2) = 8334</li>
<li>D(10^6,10^3,10^3) = 38162302</li>
</ul>
Find D(10^9,10^5,10^5).


## 解决方案


## 代码


