---
title: Project Euler 230
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    




# Project Euler 230
## 题目
### Fibonacci Words

For any two strings of digits, $A$ and $B$, we define $F_{A,B}$ to be the sequence $(A,B,AB,BAB,ABBAB,\dots)$ in which each term is the concatenation of the previous two.

Further, we define $D_{A,B}(n)$ to be the $n^{\text{th}}$ digit in the first term of $F_{A,B}$ that contains at least $n$ digits.
Example:

Let $A=1415926535, B=8979323846$. We wish to find $D_{A,B}(35)$, say.

The first few terms of F_A,B are:

$1415926535$<br>
$8979323846$<br>
$14159265358979323846$<br>
$897932384614159265358979323846$<br>
$1415926535897932384689793238461415\color{red}{9}$ $265358979323846$

Then $D_{A,B}(35)$ is the $35^{\text{th}}$ digit in the fifth term, which is $9$.

Now we use for $A$ the first $100$ digits of $\pi$ behind the decimal point:

1415926535897932384626433832795028841971693993751058209749445923078164062862089986280348253421170679 

and for B the next hundred digits:

8214808651328230664709384460955058223172535940812848111745028410270193852110555964462294895493038196 .

Find $\sum_{n = 0,1,\dots,17}  10^n\times D_{A,B}((127+19n)\times7^n)$.


## 解决方案


## 代码


