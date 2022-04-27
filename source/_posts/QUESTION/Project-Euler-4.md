---
title: Project Euler 4
tags:
  - Project Euler
mathjax: true
date: 2022-04-26 18:35:14
---

<escape><!-- more --></escape>

# Project Euler 4

## 题目

### Largest palindrome product

A palindromic number reads the same both ways. The largest palindrome made from the product of two 2-digit numbers is $9009 = 91 \times 99$.

Find the largest palindrome made from the product of two 3-digit numbers.

## 解决方法

直接枚举所有的三位数和三位数的乘积，然后再判断乘积的值是否为回文字符串即可。

## 代码

```Python
N = 3
ans = 0
for i in range(10**(N-1), 10**N):
    for j in range(10**(N-1), 10**N):
        s = i * j
        if str(s) == str(s)[::-1]:
            ans = max(ans, s)
print(ans)
```
