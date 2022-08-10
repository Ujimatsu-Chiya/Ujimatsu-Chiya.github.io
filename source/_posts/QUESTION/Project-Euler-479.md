---
title: Project Euler 479
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-05 09:29:30
---

<escape><!-- more --></escape>

# Project Euler 479

## 题目

### Roots on the Rise

Let $a_k$, $b_k$, and $c_k$ represent the three solutions (real or complex numbers) to the equation

$\dfrac{1}{x}=\left(\dfrac{k}{x}\right)^2(k+x^2)-kx$.

For instance, for $k=5$, we see that $\{a_5, b_5, c_5 \}$ is approximately $\{5.727244, -0.363622+2.057397i, -0.363622-2.057397i\}$.

Let $\displaystyle S(n) = \sum_{p=1}^n\sum_{k=1}^n(a_k+b_k)^p(b_k+c_k)^p(c_k+a_k)^p$.

Interestingly, $S(n)$ is always an integer. For example, $S(4) = 51160$.

Find $S(10^6) \text{ modulo }1\,000\,000\,007$.

## 解决方案

经过去分母和移项，原方程转化为$kx^3-k^2x^2+x-k^3=0(x \neq 0)$。

根据该[页面](https://en.wikipedia.org/wiki/Vieta%27s_formulas)关于三元一次方程$ax^3+bx^2+cx+d=0$的韦达定理：

$$x_1+x_2+x_3=-\dfrac{b}{a},x_1x_2+x_2x_3+x_1x_3=\dfrac{c}{a},x_1x_2x_3=-\dfrac{d}{a}$$

得到：

$$a_k+b_k+c_k=k,a_kb_k+b_kc_k+c_ka_k=\dfrac{1}{k},a_kb_kc_k=k^2$$

那么

$$(a_k+b_k)(b_k+c_k)(a_k+c_k)=(a_k+b_k+c_k)(a_kb_k+b_kc_k+c_ka_k)-a_kb_kc_k=1-k^2$$

因此再根据等比数列求和公式，有

$$S(n)=\sum_{k=1}^n\sum_{p=1}^n(1-k^2)^p=-\sum_{k=1}^n\dfrac{(1-k^2)((1-k^2)^n-1)}{k^2}$$

## 代码

```py
N = 10**6
mod = 10 ** 9 + 7

ans = 0
for k in range(2, N + 1):
    ans = (ans - (1 - k * k) * (pow(1 - k * k, N, mod) - 1) % mod * pow(k * k, mod - 2, mod)) % mod
print(ans)

```
