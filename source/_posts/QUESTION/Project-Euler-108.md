---
title: Project Euler 108
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:23:46
---

<escape><!-- more --></escape>

# Project Euler 108

## 题目

### Diophantine reciprocals I

In the following equation $x, y$, and $n$ are positive integers.

$$\dfrac{1}{x} + \dfrac{1}{y} = \dfrac{1}{n}$$

For $n = 4$ there are exactly three distinct solutions:

$$\begin{aligned}
\dfrac{1}{5} + \dfrac{1}{20} &= \dfrac{1}{4}\\
\dfrac{1}{6} + \dfrac{1}{12} &= \dfrac{1}{4}\\
\dfrac{1}{8} + \dfrac{1}{8} &= \dfrac{1}{4}
\end{aligned}
$$

What is the least value of $n$ for which the number of distinct solutions exceeds one-thousand?

<p class="note">NOTE: This problem is an easier version of <a href="problem=110">Problem 110</a>; it is strongly advised that you solve this one first.

## 解决方案

先暴力枚举出前几项的解的个数，然后查询OEIS，发现结果为数列[A018892](https://oeis.org/A018892)。

在FORMULA一栏中可以发现：

```
If n = (p1^a1)(p2^a2)...(pt^at), a(n) = ((2*a1 + 1)(2*a2 + 1) ... (2*at + 1) + 1)/2.
```

这说明，如果正整数$n$分解为$n=\prod p_i^{e_i}$，那么本题解的个数为$f(n)=\dfrac{(\prod 2e_i+1)+1}{2}$。

因此，通过$n$的分解质因数枚举$n$即可，枚举时，为使$n$取到的最小，注意当$e_i>e_j$时，那么$p_i<p_j$。

关于上面的式子得出过程：

将式子$\dfrac{1}{x}+\dfrac{1}{y}=\dfrac{1}{n}$进行去除分母，再进行移项后得到：$x=\dfrac{ny}{y-n}$.

令$t=y-n$，那么$y=n+t$，代入原式子，得到：$x=\dfrac{n(n+t)}{t}=\dfrac{n^2}{t}+n$.

如果$x$是一个整数，那么$t |n^2$。

那么，$t$取遍$n^2$的各个因数，根据因数个数定理，$x$有$d(n^2)=\prod 2e_i+1$种取值。

为不失解的一般性，方程$\dfrac{1}{x} + \dfrac{1}{y} = \dfrac{1}{n}$中的每个解都需要满足$x\leq y$。

而当$x=y=2n$时，满足该等于号。

故方程$\dfrac{1}{x}+\dfrac{1}{y}=\dfrac{1}{n}$解的总个数为$f(n)=\dfrac{(\prod 2e_i+1)+1}{2}$。

## 代码

```py
from tools import get_prime

N = 1000
pr = get_prime(len(bin(N)) * 50)
ans = N ** 10


def dfs(n: int, mul: int, f: int, lm: int):
    global ans
    if (mul + 1) >> 1 >= N:
        ans = n
        return
    for i in range(1, lm + 1):
        n *= pr[f]
        if n > ans:
            break
        dfs(n, mul * (2 * i + 1), f + 1, i)


dfs(1, 1, 0, N)
print(ans)

```
