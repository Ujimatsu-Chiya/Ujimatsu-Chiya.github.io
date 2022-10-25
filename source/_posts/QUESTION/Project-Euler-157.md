---
title: Project Euler 157
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-11 19:27:59
---

<escape><!-- more --></escape>
    

# Project Euler 157
## 题目
### Solving the diophantine equation $\dfrac{1}{a}+\dfrac{1}{b}=\dfrac{p}{10^n}$
Consider the diophantine equation $\dfrac{1}{a}+\dfrac{1}{b}=\dfrac{p}{10^n}$ with $a, b, p, n$ positive integers and $a \leq b$.

For $n=1$ this equation has $20$ solutions that are listed below:

||||||
|-|-|-|-|-|
|$\dfrac{1}{1}+\dfrac{1}{1}=\dfrac{20}{10}$|$\dfrac{1}{1}+\dfrac{1}{2}=\dfrac{15}{10}$|$\dfrac{1}{1}+\dfrac{1}{5}=\dfrac{12}{10}$|$\dfrac{1}{1}+\dfrac{1}{10}=\dfrac{11}{10}$|$\dfrac{1}{2}+\dfrac{1}{2}=\dfrac{10}{10}$|
|$\dfrac{1}{2}+\dfrac{1}{5}=\dfrac{7}{10}$|$\dfrac{1}{2}+\dfrac{1}{10}=\dfrac{6}{10}$|$\dfrac{1}{3}+\dfrac{1}{6}=\dfrac{5}{10}$|$\dfrac{1}{3}+\dfrac{1}{15}=\dfrac{4}{10}$|$\dfrac{1}{4}+\dfrac{1}{4}=\dfrac{5}{10}$|
|$\dfrac{1}{4}+\dfrac{1}{20}=\dfrac{3}{10}$|$\dfrac{1}{5}+\dfrac{1}{5}=\dfrac{4}{10}$|$\dfrac{1}{5}+\dfrac{1}{10}=\dfrac{3}{10}$|$\dfrac{1}{6}+\dfrac{1}{30}=\dfrac{2}{10}$|$\dfrac{1}{10}+\dfrac{1}{10}=\dfrac{2}{10}$|
|$\dfrac{1}{11}+\dfrac{1}{110}=\dfrac{1}{10}$|$\dfrac{1}{12}+\dfrac{1}{60}=\dfrac{1}{10}$|$\dfrac{1}{14}+\dfrac{1}{35}=\dfrac{1}{10}$|$\dfrac{1}{15}+\dfrac{1}{30}=\dfrac{1}{10}$|$\dfrac{1}{20}+\dfrac{1}{20}=\dfrac{1}{10}$|

How many solutions has this equation for $1 \leq n \leq 9$?


## 解决方案
将$p$移项，得到$\dfrac{1}{pa}+\dfrac{1}{pb}=\dfrac{1}{10^n}$，这是方程$\dfrac{1}{x}+\dfrac{1}{y}=\dfrac{1}{n}$的一个具体例子。

解该方程的方法在108题中提到：

- 将式子$\dfrac{1}{x}+\dfrac{1}{y}=\dfrac{1}{n}$进行去除分母，再进行移项后得到：$x=\dfrac{ny}{y-n}$.

- 令$t=y-n$，那么$y=n+t$，代入原式子，得到：$x=\dfrac{n(n+t)}{t}=\dfrac{n^2}{t}+n$.

- 如果$x$是一个整数，那么$t \mid n^2$。

- 那么，$t$取遍$n^2$的各个因数，$x$也取遍不同的值。

回到本题，我们可以枚举出$10^n$的所有因子，从而解得$x$和$y$（也就是$pa$和$pb$）的值。令$g=\gcd(x,y)$，那么$g$中的每一个因数$p$，都会对答案做出一次贡献。所有贡献相加即可。


## 代码


```py
from tools import divisors, divisors_sigma, gcd

N = 9
ans = 0
for n in [10 ** i for i in range(1, N + 1)]:
    for t in divisors(n * n):
        if t <= n:
            # divisors_sigma(n,0) 返回n的因子个数。
            ans += divisors_sigma(gcd(n * n // t + n, n + t),0)
print(ans)

```