---
title: Project Euler 203
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-30 20:28:05
---

<escape><!-- more --></escape>

# Project Euler 203

## 题目

### Squarefree Binomial Coefficients

The binomial coefficients $\displaystyle \binom n k$ can be arranged in triangular form, Pascal's triangle, like this:

||||||||||||||||
|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
||||||||1||||||||
|||||||1||1|||||||
||||||1||2||1||||||
|||||1||3||3||1|||||
||||1||4||6||4||1||||
|||1||5||10||10||5||1|||
||1||6||15||20||15||6||1||
|1||7||21||35||35||21||7||1|
||||||||...||||||||

It can be seen that the first eight rows of Pascal's triangle contain twelve distinct numbers: $1, 2, 3, 4, 5, 6, 7, 10, 15, 20, 21$ and $35$.

A positive integer $n$ is called squarefree if no square of a prime divides $n$.

Of the twelve distinct numbers in the first eight rows of Pascal's triangle, all except $4$ and $20$ are squarefree.

The sum of the distinct squarefree numbers in the first eight rows is $105$.

Find the sum of the distinct squarefree numbers in the first $51$ rows of Pascal's triangle.

## 解决方案

由于需要遍历的行数比较少，因此枚举出杨辉三角前$51$行的所有数，并直接通过因式分解判断其是否为无平方数即可。

## 代码

```py
from tools import get_pascals_triangle, factorization

N = 51
ans = 1
for x in set().union(*[ls for ls in get_pascals_triangle(N-1)]) - {1}:
    if max(f[1] for f in factorization(x)) == 1:
        ans += x
print(ans)

```
