---
title: Project Euler 160
tags:
  - Project Euler
mathjax: true
date: 2022-05-15 10:15:36
---

<escape><!-- more --></escape>

# Project Euler 160

## 题目

### Factorial trailing digits

For any $N$, let $f(N)$ be the last five digits before the trailing zeroes in $N!$.

For example,<br>
$9! = 362880$ so $f(9)=36288$<br>
$10! = 3628800$ so $f(10)=36288$<br>
$20! = 2432902008176640000$ so $f(20)=17664$

Find $f(1,000,000,000,000)$

## 解决方案

令函数$c(n)=\sum_{r\ge 1,5^r\le n} \lfloor\dfrac{n}{5^r}\rfloor$，即$n!$的后置$0$个数。容易知道，$c(n)$能够以$O(\log n)$的时间复杂度被计算出来。

令函数$g(n)=\prod_{i=1,5\nmid i}^ni$，那么可得$f(n)=g(n)f(\lfloor\dfrac{n}{5}\rfloor)\%10^5$

令函数$f_5(n)=f(n)\%5^5$，那么$f_5(n)=g(5^5)^{n/5^5}g(n\%5^5)f_5(\lfloor\dfrac{n}{5}\rfloor)\%5^5$
。

容易计算得$g(5^5)\%5^5=-1$，那么上式变成$f_5(n)=(-1)^{n/5^5}g(n\%5^5)f_5(\lfloor\dfrac{n}{5}\rfloor)\%5^5$

$f_5(n)$的值将能够迅速计算出。容易知道，只要$n$足够大，$\dfrac{n!}{10^{c(n)}}$的$2$的质因数个数将会很多。因此，可以直接假设$\dfrac{n!}{10^{c(n)}}\equiv 0(\mod 2^5)$。

根据中国剩余定理，直接解以下方程即可得到答案：

$\left\{\begin{aligned}
  & x \equiv 0 (\mod 2^5) \\
  & x \equiv f_5(n)(\mod 5^5)
\end{aligned}\right.$

但是，在$n$比较小时，需要通过暴力来规避默认$2^5$。

## 代码

```py
from tools import fac

N = 10 ** 12
M = 5
g = [1]
pw5 = 5 ** M


def f5(n):
    inv2 = (pw5 + 1) >> 1
    ans = pow(inv2, count0(N), pw5) % pw5
    while n:
        ans = ans * (-1) ** (n // pw5) * g[n % pw5] % pw5
        n //= 5
    return ans


def count0(n: int):
    ans = 0
    while n:
        ans += n // 5
        n //= 5
    return ans


if N <= M * 2 + 20 + M:
    w = str(fac(N)).rstrip('0')[-5:]
    ans = int(w)
else:
    for i in range(1, pw5):
        if i % 5 == 0:
            g.append(g[-1])
        else:
            g.append(g[-1] * i % pw5)

    r5 = f5(N)
    # 293为2^5在5^5上的逆元，29为5^5在2^5上的逆元。
    ans = (r5 * (2 ** M) * 293 + 0 * (5 ** M) * 29) % 10 ** 5
print(ans)

```
