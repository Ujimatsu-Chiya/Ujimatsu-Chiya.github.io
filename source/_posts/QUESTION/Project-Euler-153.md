---
title: Project Euler 153
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-11 19:27:48
---

<escape><!-- more --></escape>

# Project Euler 153

## 题目

### Investigating Gaussian Integers

As we all know the equation $x^2=-1$ has no solutions for real $x$.

If we however introduce the imaginary number $i$ this equation has two solutions: $x=i$ and $x=-i$.

If we go a step further the equation $(x-3)^2=-4$ has two complex solutions: $x=3+2i$ and $x=3-2i$.

$x=3+2i$ and $x=3-2i$ are called each others’ complex conjugate.

Numbers of the form a+bi are called complex numbers.

In general a+bi and a−bi are each other’s complex
conjugate.

A Gaussian Integer is a complex number a+bi such that both a and b are integers.

The regular integers are also Gaussian integers (with $b=0$).

To distinguish them from Gaussian integers with $b \neq 0$ we call such integers “rational integers.”

A Gaussian integer is called a divisor of a rational integer $n$ if the result is also a Gaussian integer.

If for example we divide $5$ by $1+2i$ we can simplify $\dfrac{5}{1+2i}$ in the following manner:

Multiply numerator and denominator by the complex conjugate of $1+2i$: $1−2i$.

The result is $\dfrac{5}{1 + 2i} = \dfrac{5}{1 + 2i}\dfrac{1 - 2i}{1 - 2i} = \dfrac{5(1 - 2i)}{1 - (2i)^2} = \dfrac{5(1 - 2i)}{1 - (-4)} = \dfrac{5(1 - 2i)}{5} = 1 - 2i$.

So $1+2i$ is a divisor of $5$.

Note that $1+i$ is not a divisor of $5$ because $\dfrac{5}{1 + i} = \dfrac{5}{2} - \dfrac{5}{2}i$.

Note also that if the Gaussian Integer ($a+bi$) is a divisor of a rational integer $n$, then its complex conjugate ($a−bi$) is also a divisor of $n$.
In fact, $5$ has six divisors such that the real part is positive: $\{1, 1 + 2i, 1 − 2i, 2 + i, 2 − i, 5\}$.

The following is a table of all of the divisors for the first five positive rational integers:

|n|Gaussian integer divisors with positive real part|Sum $s(n)$ of these divisors|
|-|-|-|
|$1$|$1$|$1$|
|$2$|$1, 1+i, 1-i, 2$|$5$|
|$3$|$1, 3$|$4$|
|$4$|$1, 1+i, 1-i, 2, 2+2i, 2-2i,4$|$13$|
|$5$|$1, 1+2i, 1-2i, 2+i, 2-i, 5$|$12$|

For divisors with positive real parts, then, we have: $\sum \limits_{n = 1}^{5} {s(n)} = 35$.
For $\sum \limits_{n = 1}^{10^5} {s(n)} = 17924657155$.
What is $\sum \limits_{n = 1}^{10^8} {s(n)}$?

## 解决方案

假设$N=10^8$。

对于一个高斯整数$z=a+bi$，令$g=\gcd(a,b)$，那么$z=g(a'+b'i),\gcd(a',b')=1$。不难发现，如果$z$是某个整数的因子，当且仅当$z$是$z(a'-b'i)=g(a^2+b^2)$的因子。问题可以转化为：一个高斯整数$a+bi$将会对答案做出多少次贡献？

枚举所有满足以下条件的高斯整数$a'-b'i$，数组$s[m]$归类并记录以下高斯整数的实部之和：

1. $\gcd(a',b')=1$
2. $a'>0,b'\ge 0$
3. $m=a'^2+b'^2$

从小到大遍历$m$时，它里面是所有不同的$a'-b'i$的和的实数部分。那么再枚举此时的$g$，那么$s[m]\cdot g$就是所有因子$g(a'+b'i)=a+bi$的实部之和，它们都是$g(a'^2+b'^2)=mg$的因子，而在$1\sim N$中，有$\left\lfloor\dfrac{N}{mg}\right\rfloor$个数是$mg$的倍数，这些因子都会出现$\left\lfloor\dfrac{N}{mg}\right\rfloor$次。

因此，最终答案为

$$\sum_{m=1}^N\sum_{g=1}^{\left\lfloor\frac{N}{m}\right\rfloor}s[m]\cdot g\cdot \dfrac{N}{mg}$$

为了能够尽快计算出$s$数组，需要做以下事情：

1. 三个特殊高斯整数$1+0i,1+1i,1-1i$要预处先记录在$s$中，它们的实部和虚部的最大公因数都是$1$。
2. 本质上，每一对数$(x,y)(x>y>0)$都可以做出$2(x+y)$的贡献，这是因为它可以提供四个高斯整数：$x+yi,x-yi,y+xi,y-xi$。这将枚举量减少到了原来的$\dfrac{1}{4}$.

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 100000000;
// s[m]记录所有复数a+bi满足|a+bi|=m,gcd(a,b)=1,a>0的实部和。
ll s[N+4];
int main() {
    ll ans = 0;
    s[1] = 1;s[2] = 2;
    for (int i = 1; i * i <= N; i++) {
        for (int j = i + 1; i * i + j * j <= N; j++) {
            if (__gcd(i, j) == 1) {
                s[i * i + j * j] += 2 * i + 2 * j;
            }
        }
    }
    for (int i = 1; i <= N; i++)
        if (s[i] > 0)
            for (int g = 1; g * i <= N; g++)
                ans += g * s[i] * (N / (g * i));
    printf("%lld\n", ans);
}

```
