---
title: Project Euler 190
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-17 22:21:35
---

<escape><!-- more --></escape>

# Project Euler 190

## 题目

### Maximising a weighted product

Let $S_m = (x_1, x_2, \dots , x_m)$ be the $m$-tuple of positive real numbers with $x_1 + x_2 + \dots + x_m = m$ for which $P_m = x_1 *x_2^2* \dots * x_m^m$ is maximised.

For example, it can be verified that $[P_{10}] = 4112$ ([ ] is the integer part function).

Find $\sum[P_m]$ for $2 \le m \le 15$.

## 拉格朗日乘数法

[拉格朗日乘数法](https://en.wikipedia.org/wiki/Lagrange_multiplier)（等式约束，与不等式约束相对）用于求多元函数在一定约束下的极值。拉格朗日乘数法可以将一个$n$元函数和$k$个约束条件的最优化问题转化成一个解$n+k$元方程组的解的问题。引入的一组新参数$\lambda$，称为拉格朗日乘数。

令$f(x_1,x_2,\dots,x_n)$为需要求极值的多元函数，$g_1(x_1,x_2,\dots,x_n)=0$,$\dots$为$k$个等式的约束，那么构造以下$n+k$元拉格朗日函数：

$$\mathcal{L}(x_1,x_2,\dots,x_n,\lambda_1,\lambda_2,\dots,\lambda_k)=f(x_1,x_2,\dots,x_n)-\sum_{i=1}^k\lambda_ig_i(x_1,x_2,\dots,x_n)$$

问题转化成对函数$\mathcal{L}$求极值。

## 解决方案

令$f(x_1,x_2,\dots,x_m)=\prod_{i=1}^mx_i^i,g(x_1,x_2,\dots,x_m)=\sum_{i=1}^mx_i-m$。

那么利用拉格朗日乘数法，构造拉格朗日函数：

$$\mathcal{L}(x_1,x_2,\dots,x_n,\lambda)=f(x_1,x_2,\dots,x_n)-\lambda g(x_1,x_2,\dots,x_n)=\prod_{i=1}^mx_i^i-\lambda(\sum_{i=1}^mx_i-m)$$

为求最大值，对每个$x_i$求偏导数，有

$$\dfrac{\partial \mathcal{L}}{\partial x_i}=\dfrac{i \cdot f(x_1,x_2,\dots,x_n)}{x_i}-\lambda$$

令$\dfrac{\partial \mathcal{L}}{\partial x_i}=0$，得到$x_i=\dfrac{i \cdot f(x_1,x_2,\dots,x_n)}{\lambda}$。

由这个式子不难发现，$x_i$的值，都是按比例分配的，即$\forall i,j\in[1,m],\dfrac{x_i}{x_j}=\dfrac{i}{j}$。

因此根据$g$这个约束，可以得到最大值点为$x_i=\dfrac{2i}{m+1}$。

## 代码

```py
N = 15
ans = 0
for m in range(2, N + 1):
    w = 1
    for i in range(1, m + 1):
        w *= (2 * i / (m + 1)) ** i
    ans += int(w)
print(ans)

```