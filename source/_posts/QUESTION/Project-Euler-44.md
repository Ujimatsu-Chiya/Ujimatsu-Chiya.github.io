---
title: Project Euler 44
tags:
  - Project Euler
mathjax: true
date: 2022-04-30 10:31:12
---

<escape><!-- more --></escape>

# Project Euler 44

## 题目

### Pentagon numbers

Pentagonal numbers are generated by the formula, $P_n=\dfrac{n(3n−1)}{2}$. The first ten pentagonal numbers are:
$$1, 5, 12, 22, 35, 51, 70, 92, 117, 145,\dots$$

It can be seen that $P_4 + P_7 = 22 + 70 = 92 = P_8$. However, their difference, $70 − 22 = 48$, is not pentagonal.

Find the pair of pentagonal numbers, $P_j$ and $P_k$, for which their sum and difference are pentagonal and $D = |P_k − P_j|$ is minimised; what is the value of $D$?

## 解决方案

先从小到大处理五边形数和值$s$，再从小到大处理五边形数差值$d(d<s)$。

通过一个二元一次方程$a+b=s,a-b=d$解出$a$和$b$的值，如果$a$和$b$也都是五边形数，那么可以输出所需值$d$。

## 代码

```py
from itertools import count


# a+b=s,a-b=d,a-d=b
def solve():
    p = []
    st = set()
    for s in (n * (3 * n - 1) // 2 for n in count(1)):
        st.add(s)
        for d in p:
            if ((d ^ s) & 1) == 0:
                a = (d + s) >> 1
                if a in st and s - a in st:
                    return d
        p.append(s)


print(solve())

```