---
title: Project Euler 318
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 318
## 题目
### 2011 nines


Consider the real number $\sqrt 2 + \sqrt 3$.<br />
When we calculate the even powers of $\sqrt 2 + \sqrt 3$
we get:<br />
$(\sqrt 2 + \sqrt 3)^2 = 9.898979485566356 \dots $<br />
$(\sqrt 2 + \sqrt 3)^4 = 97.98979485566356 \dots $<br />
$(\sqrt 2 + \sqrt 3)^6 = 969.998969071069263 \dots $<br />
$(\sqrt 2 + \sqrt 3)^8 = 9601.99989585502907 \dots $<br />
$(\sqrt 2 + \sqrt 3)^{10} = 95049.999989479221 \dots $<br />
$(\sqrt 2 + \sqrt 3)^{12} = 940897.9999989371855 \dots $<br />
$(\sqrt 2 + \sqrt 3)^{14} = 9313929.99999989263 \dots $<br />
$(\sqrt 2 + \sqrt 3)^{16} = 92198401.99999998915 \dots $<br />

It looks as if the number of consecutive nines at the beginning of the fractional part of these powers is non-decreasing.<br />
In fact it can be proven that the fractional part of $(\sqrt 2 + \sqrt 3)^{2 n}$ approaches $1$ for large $n$.


Consider all real numbers of the form $\sqrt p + \sqrt q$ with $p$ and $q$ positive integers and $p < q$, such that the fractional part 
of $(\sqrt p + \sqrt q)^{ 2 n}$ approaches $1$ for large $n$.


Let $C(p,q,n)$ be the number of consecutive nines at the beginning of the fractional part of $(\sqrt p + \sqrt q)^{ 2 n}$.


Let $N(p,q)$ be the minimal value of $n$ such that $C(p,q,n) \ge 2011$.


Find $\displaystyle \sum N(p,q) \,\, \text{ for } p+q \le 2011$.


















 




# Project Euler 318
## 题目
### 2011 nines

Consider the real number √2+√3.<br>When we calculate the even powers of √2+√3 we get:<br>(√2+√3)^2 = 9.898979485566356\dots<br>(√2+√3)^4 = 97.98979485566356\dots<br>(√2+√3)^6 = 969.998969071069263\dots<br>(√2+√3)^8 = 9601.99989585502907\dots<br>(√2+√3)^10 = 95049.999989479221\dots<br>(√2+√3)^12 = 940897.9999989371855\dots<br>(√2+√3)^14 = 9313929.99999989263\dots<br>(√2+√3)^16 = 92198401.99999998915\dots
It looks like that the number of consecutive nines at the beginning of the fractional part of these powers is non-decreasing.<br>In fact it can be proven that the fractional part of (√2+√3)^2n approaches 1 for large n.
Consider all real numbers of the form √p+√q with p and q positive integers and p<q, such that the fractional part of (√p+√q)^2n approaches 1 for large n.
Let C(p,q,n) be the number of consecutive nines at the beginning of the fractional part of  (√p+√q)^2n.
Let N(p,q) be the minimal value of n such that C(p,q,n) \ge 2011.
Find \sumN(p,q) for p+q \le 2011.


## 解决方案


## 代码


