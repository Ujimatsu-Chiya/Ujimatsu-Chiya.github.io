---
title: Project Euler 175
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 175
## 题目
### Fractions involving the number of different ways a number can be expressed as a sum of powers of 2

Define f(0)=1 and f(<var>n</var>) to be the number of ways to write <var>n</var> as a sum of powers of 2 where no power occurs more than twice. <br /><br />

For example, f(10)=5 since there are five different ways to express 10:<br />10 = 8+2 = 8+1+1 = 4+4+2 = 4+2+2+1+1 = 4+4+1+1<br /><br />

It can be shown that for every fraction <var>p/q</var> (<var>p</var>&gt;0, <var>q</var>&gt;0) there exists at least one integer <var>n</var> such that<br /> f(<var>n</var>)/f(<var>n</var>-1)=<var>p/q</var>.<br /><br />
For instance, the smallest <var>n</var> for which f(<var>n</var>)/f(<var>n</var>-1)=13/17 is 241.<br />
The binary expansion of 241 is 11110001.<br />
Reading this binary number from the most significant bit to the least significant bit there are 4 one's, 3 zeroes and 1 one. We shall call the string 4,3,1 the <span style="font-style:italic;">Shortened Binary Expansion</span> of 241.<br /><br />
Find the Shortened Binary Expansion of the smallest <var>n</var> for which<br /> f(<var>n</var>)/f(<var>n</var>-1)=123456789/987654321.<br /><br />
Give your answer as comma separated integers, without any whitespaces.


# Project Euler 175
## 题目
### Fractions involving the number of different ways a number can be expressed as a sum of powers of 2
Define $f(0)=1$ and $f(n)$ to be the number of ways to write $n$ as a sum of powers of $2$ where no power occurs more than twice. 
For example, $f(10)=5$ since there are five different ways to express $10$:<br>$10 = 8+2 = 8+1+1 = 4+4+2 = 4+2+2+1+1 = 4+4+1+1$
It can be shown that for every fraction $p/q (p&gt;0, q&gt;0)$ there exists at least one integer $n$ such that $f(n)/f(n-1)=p/q$.
For instance, the smallest $n$ for which $f(n)/f(n-1)=13/17$ is $241$.
The binary expansion of $241$ is $11110001$.
Reading this binary number from the most significant bit to the least significant bit there are $4$ one’s, $3$ zeroes and $1$ one. We shall call the string $4,3,1$ the <i>Shortened Binary Expansion</i> of $241$.
Find the Shortened Binary Expansion of the smallest $n$ for which<br>$f(n)/f(n-1)=123456789/987654321$.
Give your answer as comma separated integers, without any whitespaces.


## 解决方案


## 代码


