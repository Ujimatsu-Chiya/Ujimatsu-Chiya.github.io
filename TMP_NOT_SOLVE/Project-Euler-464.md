---
title: Project Euler 464
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 464
## 题目
### Möbius function and intervals


The <b>Möbius function</b>, denoted <var>μ</var>(<var>n</var>), is defined as:
<ul><li><var>μ</var>(<var>n</var>) = (-1)^<var>ω</var>(<var>n</var>) if <var>n</var> is squarefree (where <var>ω</var>(<var>n</var>) is the number of distinct prime factors of <var>n</var>)</li>
<li><var>μ</var>(<var>n</var>) = 0 if <var>n</var> is not squarefree.</li>
</ul>
Let P(<var>a</var>,<var>b</var>) be the number of integers <var>n</var> in the interval [<var>a</var>,<var>b</var>] such that <var>μ</var>(<var>n</var>) = 1.<br />
Let N(<var>a</var>,<var>b</var>) be the number of integers <var>n</var> in the interval [<var>a</var>,<var>b</var>] such that <var>μ</var>(<var>n</var>) = -1.<br />
For example, P(2,10) = 2 and N(2,10) = 4.



Let C(<var>n</var>) be the number of integer pairs (<var>a</var>,<var>b</var>) such that:
<ul><li> 1 \le <var>a</var> \le <var>b</var> \le <var>n</var>,</li>
<li> 99·N(<var>a</var>,<var>b</var>) \le 100·P(<var>a</var>,<var>b</var>), and</li>
<li> 99·P(<var>a</var>,<var>b</var>) \le 100·N(<var>a</var>,<var>b</var>).</li>
</ul>
For example, C(10) = 13, C(500) = 16676 and C(10 000) = 20155319.



Find C(20 000 000).




# Project Euler 464
## 题目
### Möbius function and intervals

The **Möbius function**, denoted μ(n), is defined as:
<ul>
<li>μ(n) = (-1)^ω(n) if n is squarefree (where ω(n) is the number of distinct prime factors of n)</li>
<li>μ(n) = 0 if n is not squarefree.</li>
</ul>
Let P(a,b) be the number of integers n in the interval [a,b] such that μ(n) = 1.<br>Let N(a,b) be the number of integers n in the interval [a,b] such that μ(n) = -1.<br>For example, P(2,10) = 2 and N(2,10) = 4.
Let C(n) be the number of integer pairs (a,b) such that:
<ul>
<li>1&nbsp;\le&nbsp;a&nbsp;\le&nbsp;b&nbsp;\le&nbsp;n,</li>
<li>99·N(a,b)&nbsp;\le&nbsp;100·P(a,b),</li>
<li>99·P(a,b)&nbsp;\le&nbsp;100·N(a,b).</li>
</ul>
For example, C(10)&nbsp;=&nbsp;13, C(500)&nbsp;=&nbsp;16676 and C(10&nbsp;000)&nbsp;=&nbsp;20155319.
Find C(20&nbsp;000&nbsp;000).


## 解决方案


## 代码


