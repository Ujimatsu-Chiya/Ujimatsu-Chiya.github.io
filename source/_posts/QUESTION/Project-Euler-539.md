---
title: Project Euler 539
category:
  - Project Euler
tags:
  - OEIS
mathjax: true
date: 2022-07-27 23:49:49
---

<escape><!-- more --></escape>

# Project Euler 539

## 题目

### Odd elimination

Start from an ordered list of all integers from $1$ to $n$. Going from left to right, remove the first number and every other number afterward until the end of the list. Repeat the procedure from right to left, removing the right most number and every other number from the numbers left. Continue removing every other numbers, alternating left to right and right to left, until a single number remains.

Starting with $n = 9$, we have:

<u>1</u> 2 <u>3</u> 4 <u>5</u> 6 <u>7</u> 8 <u>9</u>

2 <u>4</u> 6 <u>8</u>

<u>2</u> 6<br />

6

Let $P(n)$ be the last number left starting with a list of length $n$.

Let $\displaystyle S(n) = \sum_{k=1}^n P(k)$

You are given $P(1)=1, P(9) = 6, P(1000)=510, S(1000)=268271$.

Find $S(10^{18}) \bmod 987654321$.

## 解决方案

通过暴力枚举前一小部分值，在OEIS中查询，发现结果为[A347325](https://oeis.org/A347325)。在`FORMULA`一栏，找到如下信息：

```
a(n) = 2 * (floor(n/2) + 1 - a(floor(n/2))) for n > 1. See Zhang's solution. - Zirui Wang, Jan 02 2022
```

这直接给出了$P(n)$的递推公式：

$$
P(n)=
\left \{\begin{aligned}
  &1  & & \text{if}\quad  n=1 \\
  &2\left(\left\lfloor\dfrac{n}{2}\right\rfloor+1-P\left(\left\lfloor\dfrac{n}{2}\right\rfloor\right)\right) & & \text{else}
\end{aligned}\right.
$$

发现在这个公式下，当$n=2k,2k+1$时，$P(n)$的计算结果都相同。因此，当$n$为偶数时，写成$S(n)=S(n-1)$。当$n$为奇数，那么令$m=\dfrac{n-1}{2}$，那么

$\begin{aligned}
S(n)&=1+\sum_{i=2}^n P(i)=1+2\sum_{i=2}^n\left(\left\lfloor\dfrac{i}{2}\right\rfloor+1-P\left(\left\lfloor\dfrac{i}{2}\right\rfloor\right)\right)\\
&=1+\sum_{i=1}^m2(2m+2-2P(m))\\
&=1+2(m(m+1)+2m-2\sum_{i=1}^mP(i))\\
&=1+2m(m+1)+4m-4S(m)\\
\end{aligned}$

最终通过递归，可以以$O(\log^2n)$的时间复杂度计算出$S(n)$。

## 代码

```py
N = 10 ** 18
mod = 987654321


def P(n):
    return 1 if n == 1 else 2 * (1 + n // 2 - P(n >> 1))


def S(n):
    if n <= 1:
        return n
    elif n % 2 == 0:
        return P(n) + S(n - 1)
    else:
        m = n >> 1
        return 2 * (m * (m + 1) + n - 1 - 2 * S(m)) + 1


ans = S(N) % mod
print(ans)

```
