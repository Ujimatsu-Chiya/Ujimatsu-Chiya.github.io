---
title: Project Euler 123
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:24:45
---

<escape><!-- more --></escape>
    


# Project Euler 123
## 题目
### Prime square remainders
Let $p_n$ be the $n^{\mathrm{th}}$ prime: $2, 3, 5, 7, 11, \dots$, and let $r$ be the remainder when $(p_n-1)^n + (p_n+1)^n$ is divided by $p_n^2$.

For example, when $n = 3, p_3 = 5$, and $4^3 + 6^3 = 280 \equiv 5 \mod 25$.

The least value of $n$ for which the remainder first exceeds $10^9$ is $7037$.

Find the least value of $n$ for which the remainder first exceeds $10^{10}$.


## 解决方案

设$r(n)=((p_n-1)^n + (p_n+1)^n) \% p_n^2$

利用在第120题推导出的一部分结论，可以发现：

$$
r(n)=
\left \{\begin{aligned}
  &2  & & \mathrm{if\quad} n \equiv 0(\mod 2) \\
  &2np_n \%p_n^2 & & \mathrm{else}
\end{aligned}\right.
$$

因此，直接从第$1$个质数开始进行枚举即可，容易发现这种$\sqrt{10^{10}}$级别的枚举将会很快找到答案。
## 代码


```py
from itertools import count
from sympy import nextprime


M = 10 ** 10
pr = 2
for i in count(1, 2):
    w = 2 * i * pr % (pr * pr)
    if w >= M:
        ans = i
        break
    pr = nextprime(pr, 2)
print(ans)

```