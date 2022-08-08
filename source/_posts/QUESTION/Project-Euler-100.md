---
title: Project Euler 100
category:
  - Project Euler
tags:
  - 佩尔方程
mathjax: true
date: 2022-05-03 09:22:25
---


<escape><!-- more --></escape>

# Project Euler 100

## 题目

### Arranged probability

If a box contains twenty-one coloured discs, composed of fifteen blue discs and six red discs, and two discs were taken at random, it can be seen that the probability of taking two blue discs, $P(BB) = \dfrac{15}{21}×\dfrac{14}{20} = \dfrac{1}{2}$.

The next such arrangement, for which there is exactly $50\%$ chance of taking two blue discs at random, is a box containing eighty-five blue discs and thirty-five red discs.

By finding the first arrangement to contain over $10^{12} = 1,000,000,000,000$ discs in total, determine the number of blue discs that the box would contain.

## 解决方案

假设盒子中有$n$个彩色碟子，其中$m$个为蓝色，那么得到$P(BB)=\dfrac{C_m^2}{C_n^2}=\dfrac{m(m-1)}{n(n-1)}$。

令$P(BB)=\dfrac{1}{2}$，得到方程$2m(m-1)=n(n-1)$，

最终化成：$(2n-1)^2-2(2m-1)^2=1$

令$x=2n-1,y=2m-1$，那么就化成了$x^2-2y^2=-1$，该类方程为负佩尔方程$x^2-Dy^2=-1$。

假设$x^2-Dy^2=-1$**存在**最小特解为$(x_1,y_1)$。那么，负佩尔方程的通解$(x_k,y_k)$由以下式子导出。

$$x_k+y_k\sqrt{D}=(x_{k-1}+y_{k-1}\sqrt{D})(x_1+y_1\sqrt{D})^2$$

容易发现，$x^2-2y^2=-1$的最小特解为$(1,1)$，代入上面的导出递推公式，得到通解递推公式：

$$\left \{\begin{aligned}
  & x_{k+1}=3x_k+4y_k\\
  & y_{k+1}=2x_k+3y_k
\end{aligned}\right.
$$

将$x_k=2n_k-1,y_k=2m_k-1$代入上面的两个递推式，有：
$$\left \{\begin{aligned}
  & n_{k+1}=3n_k+4m_k-3 \\
  & m_{k+1}=2n_k+3m_k-2
\end{aligned}\right.
$$

容易发现，$n_1=4,m_1=3$是原方程中的最小特解，因此按照该式子直接递推求解。

## 代码

```py
N = 10 ** 12
n, m = 4, 3
while n <= N:
    n, m = 3 * n + 4 * m - 3, 2 * n + 3 * m - 2
ans = m
print(ans)

```
