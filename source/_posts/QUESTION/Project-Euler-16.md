---
title: Project Euler 16
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-27 09:55:37
---

<escape><!-- more --></escape>

# Project Euler 16

## 题目

### Power digit sum

$2^{16} = 32768$ and the sum of its digits is $3 + 2 + 7 + 6 + 8 = 26$.
What is the sum of the digits of the number $2^{1000}$?

## 解决方案

利用Python可以计算大数的性质，可以直接将$2^{1000}$本身计算出来。

然后通过一些方法将数位提取出来相加。

## 代码

```py
N = 2 ** 1000
ans = sum(list(map(int, str(N))))
print(ans)
```
