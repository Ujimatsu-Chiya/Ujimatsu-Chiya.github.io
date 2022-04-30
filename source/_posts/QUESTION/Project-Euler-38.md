---
title: Project Euler 38
tags:
  - Project Euler
mathjax: true
date: 2022-04-27 23:32:26
---

<escape><!-- more --></escape>

# Project Euler 38

## 题目

### Pandigital multiples

Take the number 192 and multiply it by each of 1, 2, and 3:

$192 × 1 = 192$
$192 × 2 = 384$
$192 × 3 = 576$

By concatenating each product we get the $1$ to $9$ pandigital, $192384576$. We will call $192384576$ the concatenated product of $192$ and $(1,2,3)$

The same can be achieved by starting with $9$ and multiplying by $1, 2, 3, 4,$ and $5$, giving the pandigital, $918273645$, which is the concatenated product of $9$ and $(1,2,3,4,5)$.

What is the largest $1$ to $9$ pandigital $9$-digit number that can be formed as the concatenated product of an integer with $(1,2, \dots ,n)$ where $n > 1$?

## 解决方案

如果需要$n>1$，那么当任意一个数$n$，将$n$和$2n$拼接起来，长度会翻倍（很容易超过$9$），可以使用这个方法进行剪枝。

## 代码

```Python
b = "123456789"
ans = 0
for i in range(1, int(10**(len(b)/2))+4):
    t = ""
    for x in range(1, 10):
        t += str(i * x)
        if len(t) >= 9:
            break
    u = "".join((lambda x: (x.sort(), x)[1])(list(t)))
    if u == b:
        ans = max(ans, int(t))
print(ans)
```
