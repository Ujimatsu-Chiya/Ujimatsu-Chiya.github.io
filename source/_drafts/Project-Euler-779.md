---
title: Project Euler 779
category:
  - Project Euler
tags:
  - 容斥原理
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 779

## 题目

### Prime Factor and Exponent

For a positive integer $n>1$, let $p(n)$ be the smallest prime dividing $n$, and let $\alpha(n)$ be its $\mathbf{p}$**-adic order**, i.e. the largest integer such that $p(n)^{\alpha(n)}$ divides $n$.

For a positive integer $K$, define the function $f_K(n)$ by:

$$\displaystyle f_K(n)=\frac{\alpha(n)-1}{(p(n))^K}$$

Also define $\overline{f_K}$ by:

$$\displaystyle \overline{f_K}=\lim_{N \to \infty} \frac{1}{N}\sum_{n=2}^{N} f_K(n)$$

It can be verified that $\overline{f_1} \approx 0.282419756159$.

Find $\displaystyle \sum_{K=1}^{\infty}\overline{f_K}$. Give your answer rounded to $12$ digits after the decimal point.

## 解决方案

将$\overline{f_K}$进行改写：

$$\overline{f_K}=\lim_{N \to \infty} \dfrac{1}{N}\sum_{q\in P}\dfrac{1}{q^K}\cdot \sum_{p(n)=q} (\alpha(n)-1)$$

其中$P$表示一个质数集合。

假设$q$是一个质数。在所有正整数中，$p(n)=q$的比例如下（通过容斥原理不难写出）：

$$\dfrac{1}{q}\cdot\prod_{p_i\in P,p_i<q}\left(1-\dfrac{1}{p_i}\right)$$

那么，在质数$q$的倍数$n$中，有$\dfrac{q-1}{q}$的数满足$\alpha(n)=1$，有$\dfrac{1}{q}\cdot \dfrac{q-1}{q}$的数满足$\alpha(n)=2$……有$\dfrac{q-1}{q^e}$的数满足$\alpha(n)=e$。因此，$\overline{f_K}$可以进一步改写成：

$$\overline{f_K}=\sum_{q\in P} \dfrac{1}{q^K} \cdot\dfrac{1}{q}\cdot \prod_{p_i\in P,p_i<q} \left(1-\dfrac{1}{p_i}\right)\cdot \sum_{e=1}^{\infty} \dfrac{q-1}{q^e} \cdot (e-1) $$

由于$\displaystyle{\sum_{e=1}^{\infty} \dfrac{e-1}{q^e}=\dfrac{1}{(q-1)^2}}$，因此整个式子可以化简成

$$\overline{f_K}=\sum_{q\in P} \dfrac{1}{q^K} \cdot\dfrac{1}{q}\cdot \prod_{p_i\in P,p_i<q} \left(1-\dfrac{1}{p_i}\right)\cdot \dfrac{1}{q-1} $$

那么根据等比数列公式，有$\displaystyle{\sum_{K=1}^{\infty} \dfrac{1}{q^K}=\dfrac{1}{q-1}}$

那么最终化简后，得到

$$\sum_{K=1}^{\infty} \overline{f_K}=\sum_{q\in P}\dfrac{1}{q(q-1)^2} \cdot \prod_{p_i\in P,p_i<q} \left(1-\dfrac{1}{p_i}\right) $$

直接枚举质数$q$，边枚举质数$q$，边计算第二项求积式，直到级数中某一项的值小于$10^{-16}$时停止计算。

## 代码

```py
from sympy import nextprime

N = 12
eps = 10 ** -(N + 4)
mul = 1
ans = 0
p = 1
while True:
    p = nextprime(p)
    r = mul / p / (p - 1) ** 2
    if r < eps:
        break
    ans += r
    mul *= (p - 1) / p
ans = round(ans, N)
print(ans)

```
