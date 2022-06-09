---
title: Project Euler 3
tags:
  - Project Euler
mathjax: true
date: 2022-04-24 14:09:22
---

<escape><!-- more --></escape>

# Project Euler 3

## 题目

### Largest prime factor

The prime factors of $13195$ are $5, 7, 13$ and $29$.

What is the largest prime factor of the number $600851475143$ ?

## 解决方案

直接使用sympy中的分解质因数方法即可，以后将封装到自定义的tools工具包中。

## 代码

```Python
from sympy import factorint
N = 600851475143
print(max(factorint(N).keys()))
```
