---
title: Project Euler 483
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 483
## 题目
### Repeated permutation


We define a <i>permutation</i> as an operation that rearranges the order of the elements {1, 2, 3, \dots, n}.
There are n! such permutations, one of which leaves the elements in their initial order.
For n = 3 we have 3! = 6 permutations:<br />
- P_1 = keep the initial order<br />
- P_2 = exchange the 1^st and 2^nd elements<br />
- P_3 = exchange the 1^st and 3^rd elements<br />
- P_4 = exchange the 2^nd and 3^rd elements<br />
- P_5 = rotate the elements to the right<br />
- P_6 = rotate the elements to the left


If we select one of these permutations, and we re-apply the <span style="text-decoration:underline;">same</span> permutation repeatedly, we eventually restore the initial order.<br />For a permutation P_i, let f(P_i) be the number of steps required to restore the initial order by applying the permutation P_i repeatedly.<br />For n = 3, we obtain:<br />- f(P_1) = 1 : (1,2,3) → (1,2,3)<br />- f(P_2) = 2 : (1,2,3) → (2,1,3) → (1,2,3)<br />- f(P_3) = 2 : (1,2,3) → (3,2,1) → (1,2,3)<br />- f(P_4) = 2 : (1,2,3) → (1,3,2) → (1,2,3)<br />- f(P_5) = 3 : (1,2,3) → (3,1,2) → (2,3,1) → (1,2,3)<br />- f(P_6) = 3 : (1,2,3) → (2,3,1) → (3,1,2) → (1,2,3)


Let g(n) be the average value of f^2(P_i) over all permutations P_i of length n.<br />g(3) = (1^2 + 2^2 + 2^2 + 2^2 + 3^2 + 3^2)/3! = 31/6 ≈ 5.166666667e0<br />g(5) = 2081/120 ≈ 1.734166667e1<br />g(20) = 12422728886023769167301/2432902008176640000 ≈ 5.106136147e3


Find g(350) and write the answer in scientific notation rounded to 10 significant digits, using a lowercase e to separate mantissa and exponent, as in the examples above.



# Project Euler 483
## 题目
### Repeated permutation

We define a permutation as an operation that rearranges the order of the elements {1, 2, 3, \dots, n}. There are n! such permutations, one of which leaves the elements in their initial order. For n = 3 we have 3! = 6 permutations:
<ul>
<li>P_1 = keep the initial order&nbsp;&nbsp;</li>
<li>P_2 = exchange the 1^st and 2^nd elements&nbsp;&nbsp;</li>
<li>P_3 = exchange the 1^st and 3^rd elements&nbsp;</li>
<li>P_4 = exchange the 2^nd and 3^rd elements&nbsp;</li>
<li>P_5 = rotate the elements to the right&nbsp;&nbsp;</li>
<li>P_6 = rotate the elements to the left&nbsp;&nbsp;</li>
</ul>
If we select one of these permutations, and we re-apply the <u>same</u> permutation repeatedly, we eventually restore the initial order.<br>For a permutation P_i, let f(P_i) be the number of steps required to restore the initial order by applying the permutation P_i repeatedly.<br>For n = 3, we obtain:
<ul>
<li>f(P_1) = 1 : (1,2,3) → (1,2,3)</li>
<li>f(P_2) = 2 : (1,2,3) → (2,1,3) → (1,2,3)</li>
<li>f(P_3) = 2 : (1,2,3) → (3,2,1) → (1,2,3)</li>
<li>f(P_4) = 2 : (1,2,3) → (1,3,2) → (1,2,3)</li>
<li>f(P_5) = 3 : (1,2,3) → (3,1,2) → (2,3,1) → (1,2,3)</li>
<li>f(P_6) = 3 : (1,2,3) → (2,3,1) → (3,1,2) → (1,2,3)</li>
</ul>
Let g(n) be the average value of f^2(P_i) over all permutations P_i of length n.
g(3) = (1^2 + 2^2 + 2^2 + 2^2 + 3^2 + 3^2)/3! = 31/6 ≈ 5.166666667e0g(5) = 2081/120 ≈ 1.734166667e1g(20) = 12422728886023769167301/2432902008176640000 ≈ 5.106136147e3
Find g(350) and write the answer in scientific notation rounded to 10 significant digits, using a lowercase e to separate mantissa and exponent, as in the examples above.


## 解决方案


## 代码


