---
title: Project Euler 245
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 245
## 题目
### Coresilience


We shall call a fraction that cannot be cancelled down a resilient fraction.

Furthermore we shall define the resilience of a denominator, $R(d)$, to be the ratio of its proper fractions that are resilient; for example, $R(12) = \dfrac{4}{11}$.

The resilience of a number $d \gt 1$ is then $\dfrac{\varphi(d)}{d - 1}$, where $\varphi$ is Euler's totient function.

We further define the **coresilience** of a number $n \gt 1$ as $C(n) = \dfrac{n - \varphi(n)}{n - 1}$.

The coresilience of a prime $p$ is $C(p) = \dfrac{1}{p - 1}$.

Find the sum of all <b>composite</b> integers $1 \lt n \le 2 \times 10^{11}$, for which $C(n)$ is a <dfn title="A fraction with numerator 1">unit fraction</dfn>.




## 解决方案

证明：如果$C(n)$是一个单位分数，那么$n$是一个无平方因子数。

假设$p$是$n$的任意一个质因子，$e$是一个最大的正整数使得$p^e|n$。

如果$C(n)$是一个单位分数，那么可以写成存在一个整数$m$，满足$m=\dfrac{n-1}{n-\varphi(n)}$

那么，$\varphi(n)$中有一个因子$p^{e-1}$。同时不难发现$p^{e-1}|n$。因此如果$m$是一个整数，那么$p^{e-1}|1$，从而得出$e=1$。

因此，$n$是一个无平方因子数。

接下来先讨论$n$只有两个质因数时的情况，也就是$n=pq$。

那么，不难写出，$\dfrac{pq-1}{p+q-1}=m$

进行一些移项后，可以写成$q(p-m)=m(p-1)+1$

那么得到$q=\dfrac{m(p-1)+1}{p-m}$

令$d=p-m$，那么可以写出$q=\dfrac{(p-d)(p-1)+1}{d}=\dfrac{p(p-1)+1}{d}-(p-1)$

因此枚举$p(p-1)+1$的所有因子$d$，计算出$q$后，判断$q$是否为质数，并且大于$p$。

## 代码


