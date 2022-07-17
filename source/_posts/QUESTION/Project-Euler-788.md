---
title: Project Euler 788
tags:
  - Project Euler
mathjax: true
date: 2022-07-17 23:11:14
---

<escape><!-- more --></escape>

# Project Euler 788

## 题目

### Dominating Numbers

A *dominating number* is a positive integer that has more than half of its digits equal.

For example, $2022$ is a dominating number because three of its four digits are equal to $2$. But $2021$ is not a dominating number.

Let $D(N)$ be how many dominating numbers are less than $10^N$.

For example, $D(4) = 603$ and $D(10) = 21893256$.

Find $D(2022)$. Give your answer modulo $1\,000\,000\,007$.

## 解决方案

考虑一个$n$位数中，主体数位出现了$m$次的数有$d(n,m)$个。那么就有

$$D(N)=\sum_{n=1}^N\sum_{m=\lfloor\frac{n}{2}\rfloor+1}^nd(n,m)$$

现在的问题则是计算$d(n,m).$

当$n=m$时，不难知道$d(n,m)=9$。当$n\neq m$时，由于最高位不能为$0$，因此分开考虑两种情况：数的最高位是否为主体数位。

1. 当最高位是主体数位时，那么主体数位只能有$9$种；其余主体数位一共有$C_{n-1}^{m-1}$种分配方法；非主体数位随意可以随意填另外$9$位数，一共有$9^{n-m}$种填法。那么总共有$9^{n-m+1}\cdot C_{n-1}^{m-1}$种方法。
2. 当最高位不是主体数位时，那么还继续区分两种情况：
a. 主体数位是$0$，那么最高位可以任意填$9$种；其余主体数位一共有$C_{n-1}^{m}$种分配方法；非主体数位还剩下$n-m-1$位，有$9^{n-m-1}$种填法。那么总共有$9^{n-m-1}\cdot C_{n-1}^{m}$种方法。
b. 主体数位不是$0$，那么最高位只能有$8$种填法，其余相同；主体数位有$9$种非$0$的情况。那么总共有$8\cdot9\cdot 9^{n-m-1}\cdot C_{n-1}^{m}$种方法。
因此，第$2$种情况总共有$9^{n-m+1}\cdot C_{n-1}^{m}$种方法。

把这两种情况合并，那么就可以知道：

$$d(n,m)=9^{n-m+1}\cdot C_n^m$$

直接预处理出杨辉三角，对上式求和即可。

## 代码

```py
from tools import get_pascals_triangle

N = 2022
mod = 10 ** 9 + 7
C = get_pascals_triangle(N, mod)
pw9 = [1]
for _ in range(N + 1):
    pw9.append(pw9[-1] * 9 % mod)
ans = 0
for n in range(1, N + 1):
    for m in range(n // 2 + 1, n + 1):
        ans = (ans + pw9[n - m + 1] * C[n][m]) % mod
print(ans)

```
