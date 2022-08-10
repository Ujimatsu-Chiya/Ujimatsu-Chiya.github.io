---
title: Project Euler 377
category:
  - Project Euler
tags:
  - 动态规划
  - 矩阵快速幂
mathjax: true
date: 2022-07-27 23:50:47
---

<escape><!-- more --></escape>

# Project Euler 377

## 题目

### Sum of digits - experience #13

There are $16$ positive integers that do not have a zero in their digits and that have a digital sum equal to $5$, namely:

$5, 14, 23, 32, 41, 113, 122, 131, 212, 221, 311, 1112, 1121, 1211, 2111$ and $11111$.

Their sum is $17891$.

Let $f(n)$ be the sum of all positive integers that do not have a zero in their digits and have a digital sum equal to $n$.

Find $\displaystyle \sum_{i=1}^{17} f(13^i)$.<br />
Give the last $9$ digits as your answer.

## 解决方案

注意这里需要求的是所有数之和。我们可以每次将一个数位拼接在一个数的后面，从而形成一个新的数。

令状态$c(i)(i\ge 0)$表示没有数位$0$且数位和为$i$的数的个数，那么不难写出如下状态转移方程：

$$
c(i)=
\left \{\begin{aligned}
  &1  & & \text{if\quad} i=0 \\
  &\sum_{d=1}^{\min(9,i)} c(i-d) & & \text{else}
\end{aligned}\right.
$$

将状态$c(i-d)$中的每一个数后面都添加一个数位$d$，那么就成为了$c(i)$中的数。

得到$c(i)$后，令状态$s(i)(i\ge 0)$表示没有数位$0$且数位和为$i$的数之和，那么不难写出如下状态转移方程：

$$
s(i)=
\left \{\begin{aligned}
  &0  & & \text{if\quad} i=0 \\
  &\sum_{d=1}^{\min(9,i)} 10s(i-d)+d\cdot c(i-d) & & \text{else}
\end{aligned}\right.
$$

拼接一个新的数位$d$后，状态$s(i-d)$中的所有数都需要左移一位，都乘$10$。这些数一共有$c(i-d)$个，故综合还需要添加$d\cdot c(i-d)$。

最终，$s(N)$可以以$O(N)$的时间复杂度计算出来。不过，对于题目要求的时间复杂度仍然不高，需要使用矩阵快速幂进行优化。

无论是$c$还是$s$，后面都有$9$项，因此这个矩阵的大小为$18$。这是一个比较大的矩阵，因此系数矩阵在此不展示，详见代码。

## 代码

```py
P = 13
N = 17
mod = 10 ** 9


def mul(a: list, b: list):
    return [[sum(a[i][k] * b[k][j] for k in range(len(b))) % mod for j in range(len(b[0]))] for i in range(len(a))]


def f(n):
    M = 18
    # s[i-9],s[i-8],s[i-7],...,s[i-1],c[i-9],c[i-8],c[i-7],...,c[i-1]
    a = [[0, 1, 13, 147, 1625, 17891, 196833, 2165227, 23817625, 1, 1, 2, 4, 8, 16, 32, 64, 128]]
    b = [[0 for _ in range(M)] for _ in range(M)]
    for i in range(9):
        b[i][8] = 10
        b[i + 9][8] = 9 - i

        b[i + 9][8 + 9] = 1
    for i in range(8):
        b[i + 1][i] = b[i + 1 + 9][i + 9] = 1
    while n:
        if n & 1:
            a = mul(a, b)
        b = mul(b, b)
        n >>= 1
    ans = a[0][0]
    return ans


ans = sum(f(P ** i) for i in range(1, N + 1)) % mod
print(ans)

```
