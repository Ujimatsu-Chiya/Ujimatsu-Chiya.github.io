---
title: Project Euler 45
tags:
  - Project Euler
mathjax: true
date: 2022-04-27 23:32:50
---

<escape><!-- more --></escape>

# Project Euler 45

## 题目

### Triangular, pentagonal, and hexagonal

Triangle, pentagonal, and hexagonal numbers are generated by the following formulae:

||||
|---|---|---|
|Triangle|$T_n=\frac{n(n+1)}{2}$|$1, 3, 6, 10, 15,\dots$|
|Pentagonal|$P_n=\frac{n(3n−1)}{2}$|$1, 5, 12, 22, 35, \dots$|
|Hexagonal|$H_n=n(2n−1)$|$1, 6, 15, 28, 45, \dots$|

It can be verified that $T_{285} = P_{165} = H_{143} = 40755$.

Find the next triangle number that is also pentagonal and hexagonal.

## 解决方案

每次先对当前(因变量，函数)进行排序。如果排完序后，发现三个函数值相同，那么说明找到了一个同时是三角形数、五边形数和六角形数的数，如果需要找下一个，就把所有自变量加一。

否则，就将函数值最小的那个函数自变量加一，以此保持三个函数值之间的大小平衡。

## 代码

```py
N = 3


def T(n):
    return (n * (n + 1)) >> 1


def P(n):
    return (n * (3 * n - 1)) >> 1


def H(n):
    return n * (2 * n - 1)


ls = [[1, T], [1, P], [1, H]]

while True:
    ls.sort(key=lambda x: x[1](x[0]))
    if ls[0][1](ls[0][0]) == ls[-1][1](ls[-1][0]):
        N -= 1
        if N == 0:
            ans = ls[0][1](ls[0][0])
            break
        ls[0][0] += 1
        ls[1][0] += 1
        ls[2][0] += 1
    else:
        ls[0][0] += 1
print(ans)

```