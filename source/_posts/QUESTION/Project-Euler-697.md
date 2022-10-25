---
title: Project Euler 697
tags:
  - 概率
category:
  - Project Euler
mathjax: true
date: 2022-08-21 23:51:29
---

<escape><!-- more --></escape>

# Project Euler 697

## 题目

### Randomly Decaying Sequence

Given a fixed real number $c$, define a random sequence $(X_n)_{n\ge 0}$ by the following random process:

- $X_0 = c$ (with probability $1$).
- For $n>0$, $X_n = U_n X_{n-1}$ where $U_n$ is a real number chosen at random between zero and one, uniformly, and independently of all previous choices $(U_m)_{m<n}$.

If we desire there to be precisely a $25\%$ probability that $X_{100}<1$, then this can be arranged by fixing $c$ such that $\log_{10} c \approx 46.27$.

Suppose now that $c$ is set to a different value, so that there is precisely a $25\%$ probability that $X_{10\,000\,000}<1$.

Find $\log_{10} c$ and give your answer rounded to two places after the decimal point.

## 解决方案

令$n=10^7$。原问题是求$c$使得$P \{c\cdot\prod_{i=1}^n U_i<1\}=0.25$。

令$V_i=-\ln U_i,v=\ln c$。那么问题就变成求$v$使得$P\{v-\sum_{i=1}^n V_i< 0\}=0.25$。

由于$U_i\sim U(0,1)$，因此$V_i$是服从参数为$1$的指数分布，即$V_i\sim \text{Exp}(1)$。

那么，随机变量$Y=\sum_{i=1}^n V_i$服从参数为$(n,1)$的[伽马分布](https://en.wikipedia.org/wiki/Gamma_distribution)，即有$Y\sim \Gamma(n,1)$。

由于目前是求$v$使得$P\{Y>v\}=0.25$，也就是$\Gamma(n,1)$的$0.75$分位点。根据伽马分布和[伽马函数](https://en.wikipedia.org/wiki/Gamma_function)的定义，随机变量$Y$的概率密度函数为

$$f_Y(x)=x^{n-1}\cdot e^{-x}$$

那么$Y$的分布函数恰好为[不完全伽马函数](https://en.wikipedia.org/wiki/Incomplete_gamma_function)$\Gamma(n,x)$。我们使用`scipy.special`库中的方法`gammainc(n,x)`来计算$\Gamma(n,x)$的值。为了确定$v$使得$\Gamma(n,v)=0.75$，使用二分法进行完成。

最终，$\dfrac{v}{\ln 10}$为答案。

## 代码

```py
from scipy.special import gammainc
from math import log

N = 10 ** 7
R = 0.25
R = 1 - R

l, r = 0, 10 ** 20
for _ in range(100):
    m = (l + r) * 0.5
    v = gammainc(N, m)
    if v < R:
        l = m
    else:
        r = m

ans = l / log(10)
print("{:.2f}".format(ans))

```
