---
title: Project Euler 235
tags:
  - Project Euler
mathjax: true
date: 2022-06-02 21:03:49
---

<escape><!-- more --></escape>

# Project Euler 235

## 题目

### An Arithmetic Geometric sequence

Given is the arithmetic-geometric sequence $u(k) = (900-3k)r^{k-1}$. Let $s(n) = \sum_{k=1\dots n}u(k)$.

Find the value of $r$ for which $s(5000) = -600,000,000,000$.

Give your answer rounded to $12$ places behind the decimal point.

## 解决方案

使用浮点数上的二分法，直接暴力对$u(k)$求和得出结果。由于等比数列的项数膨胀很快，求和之后的值又比较小，因此二分区间仅仅取在$1$和$1.01$之间。

为了省去求和过程，假设$u(k)=(Ak+B)r^{k-1}$，可以预先使用Mathematica求出$s(n)$的通项公式为（当然也可以通过错位相减法或者是裂项相消法手动求出）：

$$s(n)=\dfrac{anr^{n+1}-a(n+1)r^n+a+b(r-1)(r^n-1)}{(r-1)^2}$$

直接在这条式子上面进行二分求$r$的值。

## 代码

```py
N = -600000000000
n = 5000
l = 1.00
r = 1.01
for _ in range(100):
    q = 0.5 * (l + r)
    s = 0
    for k in range(1, n + 1):
        s += (900 - 3 * k) * (q ** (k - 1))
    if s < N:
        r = q
    else:
        l = q
ans = l
print("{:.12f}".format(ans))

```

```Mathematica
sum[(ak+b)*q^(k-1),{k,1,n}]
```

```py
N = -600000000000
n = 5000
A = -3
B = 900
l = 1.00
r = 1.01
for _ in range(100):
    q = 0.5 * (l + r)
    s = (A * n * q ** (n + 1) - A * (n + 1) * q ** n + A + B * (q - 1) * (q ** n - 1)) / (q - 1) ** 2
    if s < N:
        r = q
    else:
        l = q
ans = l
print("{:.12f}".format(ans))


```
