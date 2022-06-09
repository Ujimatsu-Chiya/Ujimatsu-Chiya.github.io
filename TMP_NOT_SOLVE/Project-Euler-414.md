---
title: Project Euler 414
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 414
## 题目
### Kaprekar constant


6174 is a remarkable number; if we sort its digits in increasing order and subtract that number from the number you get when you sort the digits in decreasing order, we get 7641-1467=6174.<br />
Even more remarkable is that if we start from any 4 digit number and repeat this process of sorting and subtracting, we'll eventually end up with 6174 or immediately with 0 if all digits are equal.<br /> 
This also works with numbers that have less than 4 digits if we pad the number with leading zeroes until we have 4 digits.<br />
E.g. let's start with the number 0837:<br />
8730-0378=8352<br />
8532-2358=6174


6174 is called the <b>Kaprekar constant</b>. The process of sorting and subtracting and repeating this until either 0 or the Kaprekar constant is reached is called the <b>Kaprekar routine</b>.


We can consider the Kaprekar routine for other bases and number of digits.<br /> 
Unfortunately, it is not guaranteed a Kaprekar constant exists in all cases; either the routine can end up in a cycle for some input numbers or the constant the routine arrives at can be different for different input numbers.<br />
However, it can be shown that for 5 digits and a base b = 6t+3≠9, a Kaprekar constant exists.<br />
E.g. base 15: (10,4,14,9,5)_15<br />
base 21: (14,6,20,13,7)_21

Define <var>C_b</var> to be the Kaprekar constant in base <var>b</var> for 5 digits.
Define the function <var>sb(i)</var> to be
<ul><li> 0 if i = <var>C_b</var> or if <var>i</var> written in base <var>b</var> consists of 5 identical digits
</li><li> the number of iterations it takes the Kaprekar routine in base <var>b</var> to arrive at <var>C_b</var>, otherwise
</li></ul>
Note that we can define <var>sb(i)</var> for all integers <var>i</var> < <var>b</var>^5. If <var>i</var> written in base <var>b</var> takes less than 5 digits, the number is padded with leading zero digits until we have 5 digits before applying the Kaprekar routine.


Define <var>S(b)</var> as the sum of <var>sb(i)</var> for 0 < <var>i</var> < <var>b</var>^5.<br />
E.g. S(15) = 5274369<br /> 
S(111) = 400668930299


Find the sum of S(6k+3) for 2 \le k \le 300.<br />
Give the last 18 digits as your answer.




# Project Euler 414
## 题目
### Kaprekar constant

6174 is a remarkable number; if we sort its digits in increasing order and subtract that number from the number you get when you sort the digits in decreasing order, we get 7641-1467=6174.<br>Even more remarkable is that if we start from any 4 digit number and repeat this process of sorting and subtracting, we’ll eventually end up with 6174 or immediately with 0 if all digits are equal.<br>This also works with numbers that have less than 4 digits if we pad the number with leading zeroes until we have 4 digits.<br>E.g. let’s start with the number 0837:<br>8730-0378=8352<br>8532-2358=6174
6174 is called the **Kaprekar constant**. The process of sorting and subtracting and repeating this until either 0 or the Kaprekar constant is reached is called the **Kaprekar routine**.
We can consider the Kaprekar routine for other bases and number of digits.<br>Unfortunately, it is not guaranteed a Kaprekar constant exists in all cases; either the routine can end up in a cycle for some input numbers or the constant the routine arrives at can be different for different input numbers.<br>However, it can be shown that for 5 digits and a base b = 6t+3≠9, a Kaprekar constant exists.<br>E.g. base 15: (10,4,14,9,5)_15<br>base 21: (14,6,20,13,7)_21
Define C_b to be the Kaprekar constant in base b for 5 digits. Define the function sb(i) to be
<ul>
<li>0 if i = C_b or if i written in base b consists of 5 identical digits</li>
<li>the number of iterations it takes the Kaprekar routine in base b to arrive at C_b, otherwise</li>
</ul>
Note that we can define sb(i) for all integers i < b^5. If i written in base b takes less than 5 digits, the number is padded with leading zero digits until we have 5 digits before applying the Kaprekar routine.
Define S(b) as the sum of sb(i) for 0 < i < b^5.<br>E.g. S(15) = 5274369<br>S(111) = 400668930299
Find the sum of S(6k+3) for 2 \le k \le 300.<br>Give the last 18 digits as your answer.


## 解决方案


## 代码


