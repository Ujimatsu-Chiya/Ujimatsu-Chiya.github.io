---
title: Project Euler 25
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-27 09:56:15
---

<escape><!-- more --></escape>

# Project Euler 25

## 题目

### $1000$-digit Fibonacci number

The Fibonacci sequence is defined by the recurrence relation:
$$F_1 = 1\quad F_2= 1$$
$$F_n = F_{n-1} + F_{n-2}$$
Hence the first 12 terms will be:
$$\begin{aligned}F_1&=1\\F_2&=1\\F_3&=2\\F_4&=3\\F_5&=5\\F_6&=8\\F_7&=13\\F_8&=21\\F_9&=34\\F_{10}&=55\\F_{11}&=89\\F_{12}&=144\\\end{aligned}$$

The $12\mathrm{th}$ term, $F_{12}$, is the first term to contain three digits.

What is the first term in the Fibonacci sequence to contain $1000$ digits?

## 解决方案

利用Python可以做大数运算的特点，直接迭代运算。

## 代码

```py
N = 1000
i = 1
a = b = 1
while True:
    if len(str(a)) == N:
        ans = i
        break
    a, b = b, a + b
    i += 1
print(ans)
```
