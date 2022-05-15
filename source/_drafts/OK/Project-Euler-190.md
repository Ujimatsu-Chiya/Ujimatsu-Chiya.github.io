---
title: Project Euler 190
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 190

## 题目

### Maximising a weighted product

Let $S_m = (x_1, x_2, \dots , x_m)$ be the $m$-tuple of positive real numbers with $x_1 + x_2 + \dots + x_m = m$ for which $P_m = x_1 *x_2^2* \dots * x_m^m$ is maximised.

For example, it can be verified that $[P_{10}] = 4112$ ([ ] is the integer part function).

Find $\sum[P_m]$ for $2 \le m \le 15$.

## 拉格朗日乘数法

[拉格朗日乘数法](https://en.wikipedia.org/wiki/Lagrange_multiplier)（等式约束，与不等式约束相对）用于求多元函数在一定约束下的极值。拉格朗日乘数法可以将一个$n$元函数和$k$个约束条件的z最优化问题转化成一个解$n+k$元方程组的解的问题。引入的一组新参数$\lambda$，称为拉格朗日乘数。

令$f(x_1,x_2,\dots,x_n)$为需要求极值的多元函数，$g_1(x_1,x_2,\dots,x_n)=0$,$\dots$为$k$个等式的约束，那么构造以下$n+k$元拉格朗日函数：

$$\mathcal{L}(x_1,x_2,\dots,x_n,\lambda_1,\lambda_2,\dots,\lambda_k)=f(x_1,x_2,\dots,x_n)-\sum_{i=1}^k\lambda_ig_i(x_1,x_2,\dots,x_n)$$

问题转化成对函数$\mathcal{L}$求极值。

## 解决方案

令$f(x_1,x_2,\dots,x_m)=\prod_{i=1}^mx_i^i,g(x_1,x_2,\dots,x_m)=\sum_{i=1}^mx_i-m$。

那么利用拉格朗日乘数法，构造拉格朗日函数：

// 有错
$$\mathcal{L}(x_1,x_2,\dots,x_n,\lambda)=f(x_1,x_2,\dots,x_n)-\lambda g(x_1,x_2,\dots,x_n)=\sum_{i=1}^m(x_i^i-\lambda x_i)-m$$

为求最大值，对每个$x_i$求偏导数，有

$$\dfrac{\partial \mathcal{L}}{\partial x_i}=$$
## 代码
