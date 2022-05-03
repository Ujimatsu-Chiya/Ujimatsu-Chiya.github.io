---
title: Project Euler 9
tags:
  - Project Euler
mathjax: true
date: 2022-04-26 18:35:28
---

<escape><!-- more --></escape>

# Project Euler 9

## 题目

### Special Pythagorean triplet

A Pythagorean triplet is a set of three natural numbers, $a < b < c$, for which,

$$a^2 + b^2 = c^2$$

For example, $32 + 42 = 9 + 16 = 25 = 52$.

There exists exactly one Pythagorean triplet for which $a + b + c = 1000$.

Find the product $abc$.

## 解决方案

设$n=1000$，并联立以下两个方程：
$$\left \{
\begin{aligned}
a^2 + b^2 &= c^2\\
a+b+c &=n
\end{aligned}
\right.
$$
可以得到$b$关于$a$的关系：
$$b=\dfrac{n^2-2an}{2(n-a)}$$

因此，由$a$可以直接计算出$b$。通过判断$b$是否为整数，然后计算出$c$，再判断是否满足$a<b<c$即可。

## 代码

```py
N = 1000
ans = 0
for a in range(1, N // 3):
    if (N * N - 2 * a * N) % (2 * N - 2 * a) == 0:
        b = (N * N - 2 * a * N) // (2 * N - 2 * a)
        c = N - a - b
        if a < b < c:
            ans += a * b * c
print(ans)
```
