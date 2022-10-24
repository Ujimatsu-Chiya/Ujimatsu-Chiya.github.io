---
title: Project Euler 778
category:
  - Project Euler
mathjax: true
date: 2022-08-21 23:50:39
tags:
  - 动态规划
  - 矩阵快速幂
---

<escape><!-- more --></escape>

# Project Euler 778

## 题目

### Freshman's Product

If $a,b$ are two nonnegative integers with decimal representations $a=(\dots a_2a_1a_0)$ and $b=(\dots b_2b_1b_0)$ respectively, then the *freshman's product* of $a$ and $b$, denoted $a\boxtimes b$, is the integer $c$ with decimal representation $c=(\dots c_2c_1c_0)$ such that $c_i$ is the last digit of $a_i\cdot b_i$.

For example, $234 \boxtimes 765 = 480$.

Let $F(R,M)$ be the sum of $x_1 \boxtimes \dots \boxtimes x_R$ for all sequences of integers $(x_1,\dots,x_R)$ with $0\leq x_i \leq M$.

For example, $F(2, 7) = 204$, and $F(23, 76) \equiv 5870548 \pmod{ 1\,000\,000\,009}$.

Find $F(234567,765432)$, give your answer modulo $1\,000\,000\,009$

## 解决方案

需要注意的是，本题中的每一个数位都是独立的，因此我们考虑计算出每个数位。

假设$M$是一个$l$位数$m_{l-1}m_{l-2}\dots m_0$。我们考虑单独计算$0\sim n$这些数中有多少个**有前导**$0$的数的第$k$个数位为$d$，记为$g(n,k,d)$。那么通过三部分考虑，可以写出$g$为：

$$
g(n,k,d)=
\left \{\begin{aligned}
  &\left\lfloor\dfrac{n}{10^{k+1}}\right\rfloor\cdot 10^k & & \text{if}\quad  m_k<d \\
  &\left\lfloor\dfrac{n}{10^{k+1}}\right\rfloor\cdot 10^k + n \% 10^k+1 & & \text{else if}\quad  m_k=d \\
  &\left\lfloor\dfrac{n}{10^{k+1}}\right\rfloor\cdot 10^k+10^k & & \text{else}
\end{aligned}\right.
$$

单独考虑序列$x$中所有数的第$k$位。令状态$f_k(i,j)(0\le i\le R,0< j <10)$序列$x_1,x_2,\dots,x_i$的第$k$位有多少种填法，使得$x_1\boxtimes x_2\boxtimes\dots\boxtimes x_i$的第$k$位为$j$。那么不难写出状态转移方程为

$$
f_k(i,j)=
\left \{\begin{aligned}
  &1 & & \text{if}\quad  i=0\land j=1 \\
  &0 & & \text{else if}\quad  i=0 \\
  &\sum_{\substack{0<d,m<10,\\
  m\cdot d\%10=j}}f_k(i-1,m)\cdot g(M,k,d)  & & \text{else}
\end{aligned}\right.
$$

对于方程最后一行，序列$x_i$的第$k$位有$g(M,k,d)种填法$，从而将$f_k(i-1,j)$转移到$f_k(i,j)$。

使用矩阵快速幂，可以将$f_k(R,\cdot)$以$O(\log R)$的时间复杂度计算出来。

因此最终答案为：

$$F(R,M)=\sum_{k=0}^{l-1}10^k\cdot\sum_{i=0}^{9} i\cdot f_k(R,i)$$

## 代码

```py
from itertools import count

R = 234567
M = 765432
mod = 1000000009


def cal(n, pos, d):
    pw = 10 ** pos
    ans = n // (pw * 10) * pw
    t = n // pw % 10
    if t > d:
        ans += pw
    elif t == d:
        ans += n % pw + 1
    return ans


def mul(a: list, b: list):
    return [[sum(a[i][k] * b[k][j] for k in range(len(b))) % mod for j in range(len(b[0]))] for i in range(len(a))]


ans = 0
for p in count(0, 1):
    if 10 ** p > M:
        break
    a = [[0 for _ in range(10)]]
    a[0][1] = 1
    b = [[0 for _ in range(10)] for _ in range(10)]
    for d in range(10):
        k = cal(M, p, d)
        for i in range(10):
            b[i][i * d % 10] += k
    r = R
    while r:
        if r & 1:
            a = mul(a, b)
        b = mul(b, b)
        r >>= 1
    ans += sum(i * a[0][i] for i in range(10)) * (10 ** p)
    ans %= mod
print(ans)

```
