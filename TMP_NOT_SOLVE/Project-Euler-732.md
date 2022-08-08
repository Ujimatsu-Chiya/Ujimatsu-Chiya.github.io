---
title: Project Euler 732
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 732
## 题目
### Standing on the shoulders of trolls



$N$ trolls are in a hole that is $D_N$ cm deep. The $n$-th troll is characterized by:

<ul><li>the distance from his feet to his shoulders in cm, $h_n$</li>
<li>the length of his arms in cm, $l_n$</li>
<li>his IQ (Irascibility Quotient), $q_n$.</li>
</ul>
Trolls can pile up on top of each other, with each troll standing on the shoulders of the one below him. A troll can climb out of the hole and escape if his hands can reach to the surface. Once a troll escapes he cannot participate any further in the escaping effort.


The trolls execute an optimal strategy for maximizing the total IQ of the escaping trolls, defined as $Q(N)$.


Let<br />
$r_n = \left[ \left( 5^n \bmod (10^9 + 7) \right) \bmod 101 \right] + 50$
<br />
$h_n = r_{3n}$
<br />
$l_n = r_{3n+1}$
<br />
$q_n = r_{3n+2}$
<br />
$D_N = \frac{1}{\sqrt{2}} \sum_{n=0}^{N-1} h_n$.


For example, the first troll ($n=0$) is 51cm tall to his shoulders, has 55cm long arms, and has an IQ of 75.


You are given that $Q(5) = 401$ and $Q(15)=941$.


Find $Q(1000)$.


# Project Euler 732
## 题目
### Standing on the shoulders of trolls

$N$ trolls are in a hole that is $D_N$ cm deep. The $n$-th troll is characterized by:
<ul>
<li>the distance from his feet to his shoulders in cm, $h_n$</li>
<li>the length of his arms in cm, $l_n$</li>
<li>his IQ (Irascibility Quotient), $q_n$.</li>
</ul>
Trolls can pile up on top of each other, with each troll standing on the shoulders of the one below him. A troll can climb out of the hole and escape if his hands can reach to the surface. Once a troll escapes he cannot participate any further in the escaping effort.
The trolls execute an optimal strategy for maximizing the total IQ of the escaping trolls, defined as $Q(N)$.
Let<br>$r_n = \left[ \left( 5^n \bmod (10^9 + 7) \right) \bmod 101 \right] + 50$<br>$h_n = r_{3n}$<br>$l_n = r_{3n+1}$<br>$q_n = r_{3n+2}$<br>$D_N = \frac{1}{\sqrt{2}} \sum_{n=0}^{N-1} h_n$.
For example, the first troll ($n=0$) is $51$cm tall to his shoulders, has $55$cm long arms, and has an IQ of $75$.
You are given that $Q(5) = 401$ and $Q(15)=941$.
Find $Q(1000)$.


## 解决方案


## 代码


