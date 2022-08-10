---
title: Project Euler 435
category:
  - Project Euler
tags:
  - 矩阵快速幂
mathjax: true
date: 2022-07-27 23:50:06
---

<escape><!-- more --></escape>

# Project Euler 435

## 题目

### Polynomials of Fibonacci numbers

The **Fibonacci numbers** $\{f_n, n \ge 0\}$ are defined recursively as $f_n = f_{n-1} + f_{n-2}$ with base cases $f_0 = 0$ and $f_1 = 1$.
Define the polynomials $\{F_n, n \ge 0\}$ as $F_n(x) = \displaystyle{\sum_{i=0}^n f_i x^i}$.
For example, $F_7(x) = x + x^2 + 2x^3 + 3x^4 + 5x^5 + 8x^6 + 13x^7$, and $F_7(11) = 268\,357\,683$.
Let $n = 10^{15}$. Find the sum $\displaystyle{\sum_{x=0}^{100} F_n(x)}$ and give your answer modulo $1\,307\,674\,368\,000 \ (= 15!)$.

## 解决方案

不难看到，可以将$F_n(x)$按照斐波那契数列的定义写成如下递推式：

$$
F_n(x)=
\left \{\begin{aligned}
  &x  & & \text{if\quad} n=1 \\
  &x^2+x & & \text{else if\quad} n=2 \\
  &x^2F_{n-2}(x)+xF_{n-1}(x)+x & & \text{else}
\end{aligned}\right.
$$

只要$x$是一个定值，那么$F_{n}(x)$就可以看成是一个在$n$上的线性递推。

将递推式写成矩阵形式，那么有：

$$
\begin{bmatrix}
0 & 1 & 0\\
x^2+x & x & 1\\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
F_{n-2}(x)\\
F_{n-1}(x)\\
x
\end{bmatrix}
=
\begin{bmatrix}
F_{n-1}(x)\\
F_{n}(x)\\
x
\end{bmatrix}
$$

给定初值$F_1(x)=x$和$F_2(x)=x^2+x$，那么可以通过矩阵快速幂在$O(\log n)$的时间复杂度内计算出$F_n(x)$的值。

## 代码

```py
N = 10 ** 15
M = 100
mod = 1307674368000


def mul(a: list, b: list):
    return [[sum(a[i][k] * b[k][j] for k in range(len(b))) % mod for j in range(len(b[0]))] for i in range(len(a))]


ans = 0
for x in range(M + 1):
    a = [[x, x * x + x, x]]
    b = [[0, x * x, 0],
         [1, x, 0],
         [0, 1, 1]]
    n = N - 1
    while n:
        if n & 1:
            a = mul(a, b)
        b = mul(b, b)
        n >>= 1
    ans = (ans + a[0][0]) % mod
print(ans)

```
