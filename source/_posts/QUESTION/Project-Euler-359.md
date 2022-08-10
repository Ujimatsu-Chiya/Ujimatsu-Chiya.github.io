---
title: Project Euler 359
category:
  - Project Euler
tags:
  - OEIS
mathjax: true
date: 2022-07-12 00:16:55
---

<escape><!-- more --></escape>

# Project Euler 359

## 题目

### Hilbert’s New Hotel

An infinite number of people (numbered $1, 2, 3,$ etc.) are lined up to get a room at Hilbert’s newest infinite hotel. The hotel contains an infinite number of floors (numbered $1, 2, 3,$ etc.), and each floor contains an infinite number of rooms (numbered $1, 2, 3,$ etc.).

Initially the hotel is empty. Hilbert declares a rule on how the n^th person is assigned a room: person n gets the first vacant room in the lowest numbered floor satisfying either of the following:

- the floor is empty
- the floor is not empty, and if the latest person taking a room in that floor is person m, then m + n is a perfect square

Person $1$ gets room $1$ in floor $1$ since floor $1$ is empty.
Person $2$ does not get room $2$ in floor $1$ since $1 + 2 = 3$ is not a perfect square. Person $2$ instead gets room $1$ in floor $2$ since floor $2$ is empty. Person $3$ gets room $2$ in floor $1$ since $1 + 3 = 4$ is a perfect square.

Eventually, every person in the line gets a room in the hotel.

Define $P(f, r)$ to be $n$ if person $n$ occupies room $r$ in floor $f$, and $0$ if no person occupies the room. Here are a few examples:

$\begin{aligned}
&P(1, 1) = 1\\
&P(1, 2) = 3\\
&P(2, 1) = 2\\
&P(10, 20) = 440\\
&P(25, 75) = 4863\\
&P(99, 100) = 19454
\end{aligned}$

Find the sum of all $P(f, r)$ for all positive $f$ and $r$ such that $f \times r = 71328803586048$ and give the last $8$ digits as your answer.

## 解决方案

通过暴力枚举前几项，可以在OEIS查询到结果为[A083362](https://oeis.org/A083362)。

找到`FORMULA`一栏，给出了如下信息：

```
T(0, k) = (k+1)*(k+2)/2 for k>=0, T(n, 0) = floor((n+1)^2/2) for n>0, T(n, k+1) = (2*floor((n+1)/2) + k+1)^2 - T(n, k) for n>0 and k>=0.
```

这些信息给出的公式是以$0$为初始下标的。转化成以$1$为初始下标后，有

$$
p(f,r)=
\left \{\begin{aligned}
  &\dfrac{r(r+1)}{2}  & & \text{if}\quad f=1 \\
  &\left\lfloor\dfrac{f^2}{2}\right\rfloor & & \text{else if}\quad f>1\land r=1 \\
  &\left(2\cdot\left\lfloor\dfrac{f}{2}\right\rfloor+r-1\right)^2-p(f,r-1) & & \text{else}
\end{aligned}\right.
$$

可以看到第三条式子是一个递推式，为了加速计算的过程，我们考虑将它改写成通式。

通过Mathematica输入以下代码：

```Mathematica
RSolve[{p[r] + p[r - 1] == (2*Floor[f/2] + r - 1)^2, p[1] == Floor[f^2/2]}, p[r], r]
```

运行后得出一个很长的式子。经过化简，得到通项公式：

$$
p(f,r)=
\left \{\begin{aligned}
  &\dfrac{r(r+1)}{2} & & \text{if}\quad f=1 \\
  &\dfrac{r(r-1)}{2} +\left\lfloor\dfrac{f}{2}\right\rfloor\cdot\left(\left\lfloor\dfrac{f}{2}\right\rfloor+r-(r+f)\%2\right)& & \text{else}
\end{aligned}\right.
$$

直接进行计算即可。

## 代码
```py
from tools import divisors

N = 71328803586048
mod = 10 ** 9


def P(f, r):
    if f == 1:
        return r * (r + 1) // 2
    else:
        return r * (r - 1) // 2 + f // 2 * (f // 2 + r - (r + f) % 2) * 2


ans = sum(P(d, N // d) for d in divisors(N)) % mod
print(ans)

```