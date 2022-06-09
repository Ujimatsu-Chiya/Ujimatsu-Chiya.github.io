---
title: Project Euler 539
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 539
## 题目
### Odd elimination


Start from an ordered list of all integers from 1 to n. Going from left to right, remove the first number and every other number afterward until the end of the list. Repeat the procedure from right to left, removing the right most number and every other number from the numbers left. Continue removing every other numbers, alternating left to right and right to left, until a single number remains.


Starting with n = 9, we have:<br /><u>1</u> 2 <u>3</u> 4 <u>5</u> 6 <u>7</u> 8 <u>9</u><br />
2 <u>4</u> 6 <u>8</u><br /><u>2</u> 6<br />
6


Let <var>P</var>(<var>n</var>) be the last number left starting with a list of length <var>n</var>.<br />
Let $\displaystyle S(n) = \sum_{k=1}^n P(k)$.<br />
You are given P(1)=1, P(9) = 6, P(1000)=510, S(1000)=268271.


Find S(10^18) mod 987654321.



# Project Euler 539
## 题目
### Odd elimination

Start from an ordered list of all integers from 1 to n. Going from left to right, remove the first number and every other number afterward until the end of the list. Repeat the procedure from right to left, removing the right most number and every other number from the numbers left. Continue removing every other numbers, alternating left to right and right to left, until a single number remains.
Starting with n = 9, we have:<br><u>1</u> 2 <u>3</u> 4 <u>5</u> 6 <u>7</u> 8 <u>9</u><br>2 <u>4</u> 6 <u>8</u> <u>2</u> 6<br>6
Let P(n) be the last number left starting with a list of length n.<br>Let $\displaystyle S(n) = \sum_{k=1}^n P(k)$<br>You are given P(1)=1, P(9) = 6, P(1000)=510, S(1000)=268271.
Find S(10^18) mod 987654321.


## 解决方案


## 代码


