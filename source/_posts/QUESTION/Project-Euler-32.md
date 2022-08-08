---
title: Project Euler 32
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-27 23:32:03
---

<escape><!-- more --></escape>

# Project Euler 32

## 题目

### Pandigital products

We shall say that an n-digit number is pandigital if it makes use of all the digits $1$ to $n$ exactly once; for example, the $5$-digit number, $15234$, is $1$ through $5$ pandigital.

The product $7254$ is unusual, as the identity, $39 \times 186 = 7254$, containing multiplicand, multiplier, and product is $1$ through $9$ pandigital.

Find the sum of all products whose multiplicand/multiplier/product identity can be written as a $1$ through $9$ pandigital.

HINT: Some products can be obtained in more than one way so be sure to only include it once in your sum.

## 解决方案

先枚举第$1$个因数，后枚举第$2$个因数。再判断两个因数和积拼接后的长度是否会大于$9$.

## 代码

```py
n = 1000
c = "123456789"
st = set()
for i in range(1, n):
    j = i + 1
    while True:
        s = str(i) + str(j) + str(i * j)
        if len(s) > 9:
            break
        t = "".join((lambda x: (x.sort(), x)[1])(list(s)))
        if t == c:
            st.add(i * j)
        j += 1
    i += 1
ans = sum(st)
print(ans)
```
