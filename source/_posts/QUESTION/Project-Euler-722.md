---
title: Project Euler 722
category:
  - Project Euler
tags:
  - 论文
mathjax: true
date: 2022-08-05 21:41:39
---

<escape><!-- more --></escape>

# Project Euler 722

## 题目

### Slowly converging series

For a non-negative integer $k$, define

$$
E_k(q) = \sum\limits_{n = 1}^\infty \sigma_k(n)q^n
$$

where $\sigma_k(n) = \sum_{d \mid n} d^k$ is the sum of the $k$-th powers of the positive divisors of $n$.

It can be shown that, for every $k$, the series $E_k(q)$ converges for any $0 < q < 1$.

For example,

$\begin{aligned}
&E_1(1 - \frac{1}{2^4}) = \text{3.872155809243e2}\\
&E_3(1 - \frac{1}{2^8}) = \text{2.767385314772e10}\\
&E_7(1 - \frac{1}{2^{15}}) = \text{6.725803486744e39}
\end{aligned}$

All the above values are given in scientific notation rounded to twelve digits after the decimal point.

Find the value of $E_{15}(1 - \frac{1}{2^{25}})$.

Give the answer in scientific notation rounded to twelve digits after the decimal point.

## 解决方案

本解决方案参考了Thread中的一些内容。

题目中提到的级数是[Lambert级数](https://en.wikipedia.org/wiki/Lambert_series)。它可以进行如下变换：

$$S(n)=\sum_{n=1}^\infty a_n\cdot\dfrac{q^n}{1-q^n}=\sum_{m=1}^\infty b_m\cdot q^m$$

其中，$b$是$a$和常函数$\mathbf{1}$的[狄利克雷卷积](https://en.wikipedia.org/wiki/Dirichlet_convolution)，即$b=a*\mathbf{1}$，有$b_m=\sum_{d\mid m} a_m$.

根据[莫比乌斯反演](https://en.wikipedia.org/wiki/M%C3%B6bius_inversion_formula)，有$a=b*\mu.$代入$b_n=\sigma_k(n)$，那么得到$a_n=n^k$。

因此，原来的级数$E_k(q)$也可以写成

$$E_k(q)=\sum_{n=1}^\infty n^k\cdot\dfrac{ q^n}{1-q^n}$$

使用Mathematica中的内置[欧拉——麦克劳林公式](https://en.wikipedia.org/wiki/Euler%E2%80%93Maclaurin_formula)进行逼近即可。

根据这篇[论文](https://arxiv.org/pdf/1602.01085.pdf)的式子$(1.3)$，$E_k(q)$是$\mathscr{L}_q(s,x)=\sum_{n=1}^{\infty} \dfrac{n^sq^{nx}}{1-q^n}$的一个特例，可以写成：

$$E_k(q)=\mathscr{L}_q(k,1)$$

根据这篇论文的定理$2.2(1)$，代入$x=1$，有

$$\begin{aligned}
E_k(q)&=\sum_{n=1}^\infty n^k\cdot\dfrac{ q^n}{1-q^n}=\mathscr{L}_q(k,1)\\
&=\dfrac{\Gamma(1+k)\zeta(1+k)}{\left(\log\dfrac{1}{q}\right)^{1+k}}-\sum_{i=0}^{\infty} \dfrac{\zeta(1-k-i)}{i!} B_i(1)(\log q)^{i-1}
\end{aligned}$$

其中，

- $\Gamma(n)$是[伽马函数](https://en.wikipedia.org/wiki/Gamma_function)。当$n$为正整数时，$\Gamma(n)=(n-1)!$。
- $\zeta(s)$是[黎曼$\zeta$函数](https://en.wikipedia.org/wiki/Riemann_zeta_function)。
- $B_n(x)$是[伯努利多项式](https://en.wikipedia.org/wiki/Bernoulli_polynomials)。

这两个项中后面一项的数量级远比前一项小，因此只计算前一项的值：

$$E_k(q)\approx\dfrac{k!\cdot \zeta(1+k)}{\left(\log \dfrac{1}{q}\right)^{1+k}}$$

## 代码

```Mathematica
NumberForm[NSum[n^15*q^n/(1-q^n), {n,1,Infinity}, Method -> "EulerMaclaurin"], 13]
```

```py
from tools import fac
from sympy import zeta, log

K = 15
Q = 1 - 2 ** -25
ans = "{:.12e}".format(float(fac(K) * zeta(K + 1) / (log(1 / Q) ** (K + 1)))).replace("+", "")
print(ans)

```
