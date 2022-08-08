---
title: Project Euler 304
category:
  - Project Euler
tags:
  - 矩阵快速幂
mathjax: true
date: 2022-06-08 22:37:36
---

<escape><!-- more --></escape>

# Project Euler 304

## 题目

### Primonacci

For any positive integer $n$ the function $\text{next-prime}(n)$ returns the smallest prime $p$ such that $p>n$.

The sequence $a(n)$ is defined by:$a(1)=\text{next-prime}(10^{14})$ and $a(n)=\text{next-prime}(a(n-1))$ for $n>1$.

The fibonacci sequence $f(n)$ is defined by: $f(0)=0, f(1)=1$ and $f(n)=f(n-1)+f(n-2)$ for $n>1$.

The sequence $b(n)$ is defined as $f(a(n))$.

Find $\sum b(n)$ for $1\le n\le100 000$. Give your answer $\mod 1234567891011$.

## 解决方案

将斐波那契数的通项公式写成矩阵形式：

$$
\begin{bmatrix}
0 & 1\\
1 & 1
\end{bmatrix}
\begin{bmatrix}
f(i-2)\\
f(i-1)
\end{bmatrix}
=
\begin{bmatrix}
f(i-1)\\
f(i)
\end{bmatrix}
$$

令$B=\begin{bmatrix}
0 & 1\\
1 & 1
\end{bmatrix}$，那么通过矩阵快速幂，可以$O\log(n)$的时间复杂度内求解出第$n$项的值。

另外，上面的等式可以写成

$$
B^d
\begin{bmatrix}
f(i-d-1)\\
f(i-d)
\end{bmatrix}
=
\begin{bmatrix}
f(i-1)\\
f(i)
\end{bmatrix}
$$

这$10^5$次的询问是独立的，并且之间的间隔$d$也比较小。我们可以基于上式来减少矩阵乘法的运算次数，用上一次的结果继续转移，计算出当前结果。

求一个数的下一个质数，使用sympy的nextprime函数，效率可以接受。

## 代码

```py
from sympy import nextprime

M = 10 ** 14
Q = 10 ** 5
mod = 1234567891011


def mul(a: list, b: list):
    return [[sum(a[i][k] * b[k][j] for k in range(len(b))) % mod for j in range(len(b[0]))] for i in range(len(a))]


b_pre = [[[0, 1], [1, 1]]]
for i in range(len(bin(M+Q))+2):
    b_pre.append(mul(b_pre[-1], b_pre[-1]))


def cal(a, n):
    i = 0
    while n:
        if n & 1:
            a = mul(a, b_pre[i])
        i += 1
        n >>= 1
    return a


a = [[0, 1]]
ans = 0
pre = 0
for n in range(Q):
    M = nextprime(M)
    val = M - pre
    a = cal(a, val)
    ans = (ans + a[0][0]) % mod
    pre = M
print(ans)

```
