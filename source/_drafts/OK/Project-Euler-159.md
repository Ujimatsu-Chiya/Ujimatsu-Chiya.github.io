---
title: Project Euler 159
tags:
  - Project Euler
mathja\times: true
---
<escape><!-- more --></escape>
    


# Project Euler 159
## 题目
### Digital root sums of factorisations
A composite number can be factored many different ways. For instance, not including multiplication by one, $24$ can be factored in $7$ distinct ways:

$\begin{aligned}
24 &= 2\times2\times2\times3 \\
24 &= 2\times3\times4 \\
24 &= 2\times2\times6 \\
24 &= 4\times6 \\
24 &= 3\times8\\
24 &= 2\times12\\
24 &= 24
\end{aligned}$

Recall that the digital root of a number, in base $10$, is found by adding together the digits of that number, and repeating that process until a number is arrived at that is less than $10$. Thus the digital root of $467$ is $8$.

We shall call a Digital Root Sum (DRS) the sum of the digital roots of the individual factors of our number.

The chart below demonstrates all of the DRS values for $24$.

|Factorisation|Digital Root Sum|
|-|-|
|$2	\times2	\times2	\times3$|$9$|
|$2	\times3	\times4$|$9$|
|$2	\times2	\times6$|$10$|
|$4	\times6$|$10$|
|$3	\times8$|$11$|
|$2	\times12$|$5$|
|$24$|$6$|

The maximum Digital Root Sum of $24$ is $11$.

The function $\mathrm{mdrs}(n)$ gives the maximum Digital Root Sum of $n$. So $\mathrm{mdrs}(24)=11$.

Find $\sum \mathrm{mdrs}(n)$ for $1 < n < 1,000,000$.


## 解决方案


## 代码


