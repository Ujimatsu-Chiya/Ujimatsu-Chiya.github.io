---
title: Project Euler 53
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>



# Project Euler 53
## 题目
### Combinatoric selections


There are exactly ten ways of selecting three from five, 12345:

$$ 123, 124, 125, 134, 135, 145, 234, 235, 245, 345 $$

In combinatorics, we use the notation, $\displaystyle \binom 5 3 = 10$.
In general, $\displaystyle \binom n r = \dfrac{n!}{r!(n-r)!}$, where $r \le n$, $n! = n \times (n-1) \times \dots \times 3 \times 2 \times 1$, and $0! = 1$.

It is not until $n = 23$, that a value exceeds one-million: $\displaystyle \binom {23} {10} = 1144066$.

How many, not necessarily distinct, values of $\displaystyle \binom n r$ for $1 \le n \le 100$, are greater than one-million?
