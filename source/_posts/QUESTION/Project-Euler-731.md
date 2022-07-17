---
title: Project Euler 731
tags:
  - Project Euler
mathjax: true
date: 2022-07-17 23:11:57
---

<escape><!-- more --></escape>

# Project Euler 731

## 题目

### A Stoneham Number

$$A=\sum_{i=1}^{\infty} \frac{1}{3^i 10^{3^i}}$$

Define $A(n)$ to be the $10$ decimal digits from the $n\text{th}$ digit onward.

For example, $A(100) = 4938271604$ and $A(10^8)=2584642393$.

Find $A(10^{16})$

## 解决方案

如果要求分数$\dfrac{a}{b}$的第$n$位后的情况，那么相当于计算分数$\dfrac{a\cdot10^{n-1}}{b}$的小数情况。这相当于直接将小数点右移了$n-1$位。

并且我们不需要知道分数$\dfrac{a\cdot10^{n-1}}{b}$的整数部分。为了方便计算，就求$\dfrac{a\cdot10^{n-1}\%b}{b}$的小数部分。

回到题目中，对于一个特定的分数$\dfrac{1}{3^i\cdot 10^{3^i}}$而言，按照上面所述，转化后则变成$\dfrac{10^{n-3^i-1}}{3^i}.$那么就相当于求$\dfrac{10^{n-3^i-1}\%3^i}{3^i}$的小数部分。

最终将这些值相加即可。

## 代码

```py
from itertools import count

N = 10 ** 16
M = 10
f = 0
for i in count(0, 1):
    if N + 20 < 3 ** i + 1:
        break
    f += pow(10, N - 3 ** i - 1, 3 ** i) / 3 ** i
    f -= int(f)
ans = str(f)[2:][:10]
print(ans)

```
