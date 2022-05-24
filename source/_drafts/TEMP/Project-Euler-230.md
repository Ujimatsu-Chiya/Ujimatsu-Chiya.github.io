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

For any two strings of digits, A and B, we define F_A,B to be the sequence (A,B,AB,BAB,ABBAB,\dots) in which each term is the concatenation of the previous two.

Further, we define D_A,B(<var>n</var>) to be the <var>n</var>^th digit in the first term of F_A,B that contains at least <var>n</var> digits.

Example:

Let A=1415926535, B=8979323846. We wish to find D_A,B(35), say.

The first few terms of F_A,B are:<br />
1415926535<br />
8979323846<br />
14159265358979323846<br />
897932384614159265358979323846<br />
1415926535897932384689793238461415<span style="color:#FF0000;"><b>9</b></span>265358979323846<br />

Then D_A,B(35) is the 35^th digit in the fifth term, which is 9.

Now we use for A the first 100 digits of π behind the decimal point:
14159265358979323846264338327950288419716939937510 <br />
58209749445923078164062862089986280348253421170679 

and for B the next hundred digits:

82148086513282306647093844609550582231725359408128 <br />
48111745028410270193852110555964462294895493038196 .

Find <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span>_<var>n</var> = 0,1,\dots,17   10^<var>n</var>\times D_A,B((127+19<var>n</var>)\times7^<var>n</var>) .



 



# Project Euler 230
## 题目
### Fibonacci Words

For any two strings of digits, A and B, we define F_A,B to be the sequence (A,B,AB,BAB,ABBAB,\dots) in which each term is the concatenation of the previous two.
Further, we define D_A,B(n) to be the n^th digit in the first term of F_A,B that contains at least n digits.
Example:
Let A=1415926535, B=8979323846. We wish to find D_A,B(35), say.
The first few terms of F_A,B are:<br>1415926535<br>8979323846<br>14159265358979323846<br>897932384614159265358979323846<br>1415926535897932384689793238461415<span style="color: #FF0000"><b>9</b></span>265358979323846
Then D_A,B(35) is the 35^th digit in the fifth term, which is 9.
Now we use for A the first 100 digits of π behind the decimal point:
14159265358979323846264338327950288419716939937510<br>58209749445923078164062862089986280348253421170679 
and for B the next hundred digits:
82148086513282306647093844609550582231725359408128<br>48111745028410270193852110555964462294895493038196 .
Find \sum_n = 0,1,\dots,17 &nbsp; 10^n\times D_A,B((127+19n)\times7^n).


## 解决方案


## 代码


