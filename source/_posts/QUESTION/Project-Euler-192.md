---
title: Project Euler 192
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-24 11:02:00
---

<escape><!-- more --></escape>

# Project Euler 192

## 题目

### Best Approximations

Let x be a real number.

A best approximation to $x$ for the denominator bound $d$ is a rational number $\dfrac{r}{s}$ in reduced form, with $s \le d$, such that any rational number which is closer to $x$ than $\dfrac{r}{s}$ has a denominator larger than $d$:

$$\left|\dfrac{p}{q}-x\right| < \left|\dfrac{r}{s}-x\right| \Rightarrow q > d$$

For example, the best approximation to $\sqrt{13}$ for the denominator bound $20$ is $\dfrac{18}{5}$ and the best approximation to $\sqrt{13}$ for the denominator bound $30$ is $\dfrac{101}{28}$.

Find the sum of all denominators of the best approximations to $\sqrt{n}$ for the denominator bound $10^{12}$, where $n$ is not a perfect square and $1 < n \le 100000$.

## 解决方案

令$M=10^{12}$。如果需要求无理数$\sqrt{n}$的有理近似，那么我们将在[Stern-Brocot Tree](https://en.wikipedia.org/wiki/Stern%E2%80%93Brocot_tree)上“尝试”查找这个数。（这里使用的Stern-Brocot Tree是全体最简分数，因此最小值为$0$，最大值则推广到无穷。）

最终，寻找到两个候选答案$\dfrac{a}{c},\dfrac{b}{d}$，满足$\dfrac{a}{c}<\sqrt{n}<\dfrac{b}{d},c,d \le M$。判断这两个分数谁比较接近即可。

为了避免浮点数产生的误差，进行浮点数比较时会转成整数之间的比较：

1. 比较分数$\dfrac{p}{q}$和$\sqrt{n}$，相当于比较$p^2$和$nq^2$的大小。
2. 比较$\sqrt{n}-\dfrac{a}{c}$和$\dfrac{b}{d}-\sqrt{n}$，经转化后，相当于比较$4nc^2d^2$和$(bc+ad)^2$的大小。

另一个用有理数近似无理数的相关的方法是基于连分数的，在该[页面](https://en.wikipedia.org/wiki/Continued_fraction#Best_rational_approximations)中有介绍。

## 代码

```py
N = 10 ** 5
M = 10 ** 12


def cal(n):
    a, c = 0, 1
    b, d = 1, 0
    while True:
        p = a + b
        q = c + d

        if q > M:
            if 4 * n * c ** 2 * d ** 2 < (a * d + b * c) ** 2:
                return c
            else:
                return d
        else:
            t = p * p - q * q * n
            if t == 0:
                # 找到了一个有理数p/q，其值为sqrt(n)，这说明n是个平方数，不是我们需要求的。
                break
            if t > 0:
                b, d = p, q
            else:
                a, c = p, q
    return 0


ans = sum(cal(x) for x in range(2, N + 1))
print(ans)

```
