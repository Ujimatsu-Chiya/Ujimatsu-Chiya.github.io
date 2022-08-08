---
title: Project Euler 346
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-22 23:27:24
---

<escape><!-- more --></escape>

# Project Euler 346

## 题目

### Strong Repunits

The number $7$ is special, because $7$ is $111$ written in base $2$, and $11$ written in base $6$ (i.e. $7_{10} = 11_{6} = 111_{2}$). In other words, $7$ is a repunit in at least two bases $b > 1$.

We shall call a positive integer with this property a strong repunit. It can be verified that there are $8$ strong repunits below $50$:  $\{1,7,13,15,21,31,40,43\}$.

Furthermore, the sum of all strong repunits below $1000$ equals $15864$.

Find the sum of all strong repunits below $10^{12}$.

## 解决方案

不难发现，对于任意一个数$n>2$，$n$都可以写成$n-1$进制下的$11_{n-1}$，因此$2$个$1$是普遍情况。

那么，题目可以转化为求所有满足以下条件的数$n$之和：存在一个$b$，$n$在$b$进制下所有数位都是$1$，并且数位个数达到$3$以上。

令$N=10^{12}$。因此考虑枚举$b$，使得$n=b^2+b+1,n\le N$。在$b$进制下，当前有一个满足题目条件的答案$m$，令$m'=mb+1$，那么就产生了比$m$多一位的答案$m'$。由此枚举，最终产生所有答案。

## 代码

```py
from itertools import count

N = 10 ** 12
st = set()
for b in count(2, 1):
    n = b * b + b + 1
    if n > N:
        break
    while n <= N:
        st.add(n)
        n = n * b + 1
ans = sum(st) + 1
print(ans)

```
