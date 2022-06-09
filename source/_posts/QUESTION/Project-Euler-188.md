---
title: Project Euler 188
tags:
  - Project Euler
mathjax: true
date: 2022-05-15 10:16:03
---

<escape><!-- more --></escape>

# Project Euler 188

## 题目

### The hyperexponentiation of a number

The *hyperexponentiation* or *tetration* of a number a by a positive integer b, denoted by $a\uparrow\uparrow b$ or $^ba$, is recursively defined by:

$a\uparrow\uparrow1 = a, a\uparrow\uparrow(k+1) = a^{(a\uparrow\uparrow k)}$.

Thus we have e.g. $3\uparrow\uparrow2 = 3^3 = 27$, hence $3\uparrow\uparrow3 = 3^{27} = 7625597484987$ and $3\uparrow\uparrow4$ is roughly $10^{3.6383346400240996*10^{12}}$.

Find the last $8$ digits of $1777\uparrow\uparrow1855$.

## 欧拉降幂公式

欧拉降幂公式，用于高效计算$a^b\% m$的值（尤其$b$很大时）：

$$
a^b\equiv
\left \{\begin{aligned}
  &a^{b\% \varphi(m)}  & & \mathrm{if\quad} \gcd(a,m)=1 \\
  &a^b & & \mathrm{else if\quad} b<\varphi(m) &(\mod p)\\
  &a^{b\%\varphi(m)+\varphi(m)} & & \mathrm{else}
\end{aligned}\right.
$$

其中$\varphi$为欧拉函数。

## 解决方案

根据式子的定义，通过欧拉降幂公式直接递归计算指数，再计算出式子的值本身。可以知道，递归的层数很低。

## 代码

```py
from tools import factorization

n = 1777
m = 1855
mod = 10 ** 8


def phi(n):
    ls = factorization(n)
    for p, e in ls:
        n = n // p * (p - 1)
    return n


def dfs(a: int, f: int, mod: int):
    if f <= 1:
        return pow(a, f, mod)
    elif mod == 1:
        return 0
    else:
        ph = phi(mod)
        return pow(a, dfs(a, f - 1, ph) % ph, mod)


ans = "{:08}".format(dfs(n, m, mod))
print(ans)

```
