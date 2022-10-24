---
title: Project Euler 120
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-06 22:24:33
---

<escape><!-- more --></escape>

# Project Euler 120

## 题目

### Square remainders

Let $r$ be the remainder when $(a-1)^n + (a+1)^n$ is divided by $a^2$.

For example, if $a = 7$ and $n = 3$, then $r = 42: 6^3 + 8^3 = 728 \equiv 42 \bmod 49$. And as $n$ varies, so too will $r$, but for $a = 7$ it turns out that $r_{\max} = 42$.

For $3 \le a \le 1000$, find $\sum r_{\max}$.

## 二项式定理

二项式定理，即$n$次方二项式$(a+b)^n$的展开式：

$$(a+b)^n=\sum_{i=0}^n\dbinom{n}{i}a^ib^{n-i}$$

## 解决方案

设$r(a,n)=((a-1)^n+(a+1)^n) \% a^2$。

根据二项式定理，对$a^2$取模后，二项式展开式中$a$的次数为$2$及以上的项不考虑，只考虑$a$的次数为$0$或$1$的项。

因此，满足下式：

$r(a,n) \equiv \dbinom{n}{1}a\cdot(-1)^{n-1}+\dbinom{n}{0}(-1)^n+\dbinom{n}{1}a\cdot 1^{n-1}+\dbinom{n}{0}1^n\equiv an+1+an\cdot(n-1)^n+(-1)^n\pmod{a^2}$

可以写成：

$$
r(a,n)=
\left \{\begin{aligned}
  &2  & & \text{if}\quad n \equiv 0 \pmod 2 \\
  &2an \%a^2 & & \text{else}
\end{aligned}\right.
$$

为使得$r(a,n)$最大，故不考虑$n$为偶数的情况。那么此时可以写成$r(a,n)=a\cdot (2n \% a)$。

值$2n\%a$需要尽可能接近$a$。由于$2n$为偶数，因此当$a$为偶数时，$\gcd(a,2)=2$，因此$2n\%a$最大能只能取到$2$的倍数$a-2$，而当$a$为奇数时，$\gcd(a,2)=1$，$2n\%a$最大可以取到$1$的倍数$a-1$。

因此有：

$$
r_{\max}(a)=
\left \{\begin{aligned}
  &a(a-2)  & & \text{if}\quad a \equiv 0 \pmod 2 \\
  &a(a-1) & & \text{else}
\end{aligned}\right.
$$

## 代码

```py
N = 1000
ans = 0
for a in range(3, N + 1):
    if a & 1:
        ans += a * (a - 1)
    else:
        ans += a * (a - 2)
print(ans)
```
