---
title: Project Euler 323
category:
  - Project Euler
tags:
  - 概率
  - 动态规划
mathjax: true
date: 2022-06-02 21:03:38
---

<escape><!-- more --></escape>

# Project Euler 323

## 题目

### Bitwise-OR operations on random integers

Let $y_0, y_1, y_2,\dots$ be a sequence of random unsigned $32$ bit integers (i.e. $0 \le y_i < 2^{32}$, every value equally likely).
For the sequence $x_i$ the following recursion is given:

- $x_0 = 0$ and
- $x_i = x_{i-1} \mathbf{|} y_{i-1}$, for $i > 0$. ( $\mathbf{|}$ is the bitwise-OR operator)

It can be seen that eventually there will be an index $N$ such that
$x_i = 2^{32} -1$ (a bit-pattern of all ones) for all $i \ge N$.

Find the expected value of $N$. Give your answer rounded to $10$ digits after the decimal point.

## 解决方案

令$N=32$。

一个观察点：当前状态其实和$y_i$的值没有关系，只和$y_i$的二进制$1$的个数有关系。

因此，我们只考虑$y_i$中还有多少个$0$还没有被翻成$1$。

令$f(i)(i\ge 0)$表示还有$i$个$0$还没被翻成$1$的情况下，全都完成翻转的期望。

那么，状态$i$有$\dfrac{\binom{i}{0}}{2^i}$的概率转换成状态$i$，也就是说，一个比特都没翻转成功；有$\dfrac{\binom{i}{1}}{2^i}$的概率转换成状态$i-1$，也就是说只有一个比特翻转成功了……有$\dfrac{\binom{i}{i}}{2^i}$的概率转换成状态$0$，此时$i$个比特全部成功翻转。那么，我们可以写出如下的式子：

$$f(i)=\sum_{j=0}^i\left(\dfrac{\binom{i}{j}}{2^n}\cdot f(j)\right)+1$$

这是一个**有后效性**的动态规划方程，因为状态之间形成了循环的依赖（状态$i$依赖于自身）。不过，这种情况下消除后效性很简单。右边有一个项也是$f(i)$，只需要挪到左边消除就可以完成消除后效性，从而正确计算结果。

因此，可以正式写出状态转移方程：

$$
f(i)=
\left \{\begin{aligned}
  &0  & & \text{if\quad} i=0 \\
  &\dfrac{\sum_{j=0}^{i-1}\binom{i}{j}\cdot f(j)+2^i}{2^i-1} & & \text{else}
\end{aligned}\right.
$$

因此，最终结果为$f(N)$。

## 代码

```py
from tools import get_pascals_triangle

N = 32
C = get_pascals_triangle(N)
f = [0]
for n in range(1, N + 1):
    f.append(2 ** n)
    for i in range(n):
        f[n] += C[n][i] * f[i]
    f[n] /= 2 ** n - 1
ans = f[N]
print("{:.10f}".format(ans))
```
