---
title: Project Euler 40
tags:
  - Project Euler
mathjax: true
date: 2022-04-27 23:32:34
---

<escape><!-- more --></escape>

# Project Euler 40

## 题目

### Champernowne’s constant

An irrational decimal fraction is created by concatenating the positive integers:

<center style="font-family:'Courier New',monospace;">
0.12345678910<font color=red>1</font>112131415161718192021...
</center>

It can be seen that the $12$<sup>th</sup> digit of the fractional part is $1$.

If $d_n$ represents the $n$<sup>th</sup> digit of the fractional part, find the value of the following expression.

$$d_1\times d_{10} \times d_{100} \times d_{1000} \times d_{10000} \times d_{100000}\times d_{1000000}$$

## 解决方案

每一个$d_i$都是一个独立的问题，可以先计算后再相乘。

可以知道，$1\sim 9,10\sim 99,100\sim 999,\dots,10^{n-1}\sim 10^n-1,\dots$，每一块都有相同的长度，而且，每一块的长度增长都是为$1$。

因此，计算每一个独立的$d_i$时，先找到第$i$位属于那一块，然后再判断第$i$位属于哪一个数，之后直接相乘即可。

## 代码

```py
que = [10 ** i for i in range(7)]


def cal(x: int):
    x -= 1
    i = 1
    while True:
        l = 10 ** (i - 1)
        r = 10 ** i - 1
        if x >= (r - l + 1) * i:
            x -= (r - l + 1) * i
        else:
            d, pos = divmod(x, i)
            val = d + l
            ans = int(str(val)[pos])
            break
        i += 1
    return ans


ans = 1
for x in que:
    ans *= cal(x)
print(ans)
```
