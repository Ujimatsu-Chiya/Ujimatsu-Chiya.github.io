---
title: Project Euler 751
category:
  - Project Euler
tags:
  - 二分
mathjax: true
date: 2022-07-17 23:12:09
---

<escape><!-- more --></escape>

# Project Euler 751

## 题目

### Concatenation Coincidence

A non-decreasing sequence of integers $a_n$ can be generated from any positive real value $\theta$ by the following procedure:

$$\begin{aligned}
\begin{split}
b_1 &= \theta \\
b_n &= \left\lfloor b_{n-1} \right\rfloor \left(b_{n-1} - \left\lfloor b_{n-1} \right\rfloor + 1\right)~~~\forall ~ n \geq 2 \\
a_n &= \left\lfloor b_{n} \right\rfloor
\end{split}
\end{aligned}$$

Where $\left\lfloor . \right\rfloor$ is the floor function.

For example, $\theta=2.956938891377988\dots$ generates the Fibonacci sequence: $2, 3, 5, 8, 13, 21, 34, 55, 89, \dots$

The *concatenation* of a sequence of positive integers $a_n$ is a real value denoted $\tau$ constructed by concatenating the elements of the sequence after the decimal point, starting at $a_1$: $a_1.a_2a_3a_4\dots$

For example, the Fibonacci sequence constructed from $\theta=2.956938891377988\dots$ yields the concatenation $\tau=2.3581321345589\dots$ Clearly, $\tau \neq \theta$ for this value of $\theta$.

Find the only value of $\theta$ for which the generated sequence starts at $a_1=2$ and the concatenation of the generated sequence equals the original value: $\tau = \theta$. Give your answer rounded to 24 places after the decimal point.

## 解决方案

当$a_1=2$时，也就是说$\theta$的整数部分只能是$2$，也就是说$2\le\theta<3$。在这个范围内，在浮点数上二分算法逼近所求$\theta$的值。虽然这个二分算法并非正确，但是它仍然输出了正确的答案。**整体上**$\tau$的增长速度比$\theta$快。

## 代码

```py
N = 2
M = 24
l, r = N, N + 1
for _ in range(100):
    theta = 0.5 * (l + r)
    b = [theta]
    a = [int(theta)]
    for i in range(M):
        b.append(int(b[-1]) * (b[-1] - int(b[-1]) + 1))
        a.append(int(b[-1]))
    tau = str(a[0]) + "."
    for i in range(1, M):
        tau += str(a[i])
    tau = float(tau)
    if tau < theta:
        r = theta
    else:
        l = theta
ans = "{}.".format(a[0]) + "".join(str(x) for x in a[1:])[:M]
print(ans)

```
