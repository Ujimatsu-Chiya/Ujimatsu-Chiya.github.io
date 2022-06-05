---
title: Project Euler 317
tags:
  - Project Euler
mathjax: true
date: 2022-06-05 09:29:14
---

<escape><!-- more --></escape>

# Project Euler 317

## 题目

### Firecracker

A firecracker explodes at a height of $100 \text{m}$ above level ground. It breaks into a large number of very small fragments, which move in every direction; all of them have the same initial velocity of $20 \text{m/s}$.

We assume that the fragments move without air resistance, in a uniform gravitational field with $g=9.81 \text{m/s}^2$.

Find the volume (in $\text{m}^3$) of the region through which the fragments move before reaching the ground.

Give your answer rounded to four decimal places.

## 解决方案

可以发现，所要求解的物体是一个绕$y$轴旋转体。

假设抛出的物体的方向和$x$轴正方向的夹角为$\theta$，并且当前时间为$t$。那么可以列出如下$(x,y)$关于$(\theta,t)$的参数方程：

$$\left \{\begin{aligned}
  & x=vt\cos\theta\\
  & y=h+vt\sin\theta-\dfrac{1}{2}gt^2
\end{aligned}\right.$$

将$y$固定，在此约束下$t$和$\theta$要取适当的值使得$x$取到最大值，这个过程用拉格朗日乘数法解决。

因此，可以写出

$$\mathcal{L}(\lambda,\theta,t)=vt\cos\theta-\lambda(h+vt\sin\theta-\dfrac{1}{2}gt^2-y)=0$$

计算得到：

$$\dfrac{\partial \mathcal{L}}{\partial t}=v\cos\theta-\lambda v\sin\theta+\lambda gt$$

$$\dfrac{\partial \mathcal{L}}{\partial \theta}=-vt\sin\theta-\lambda vt\cos\theta$$

令$\dfrac{\partial \mathcal{L}}{\partial t}=0,\dfrac{\partial \mathcal{L}}{\partial \theta}=0$，那么得到式子$v=gt\sin\theta$。然后联立$x=vt\cos\theta,y=h+vt\sin\theta-\dfrac{1}{2}gt^2$，那么得到最终的曲线的方程：

$$x^2=\dfrac{v^2}{g}(2h+\dfrac{v^2}{g}-2y)$$

当物体从竖直向上抛出时，能够达到的高度最高，为$H=h+\dfrac{v^2}{2g}$。

因此，答案为

$$\begin{aligned}
I&=\int_{0}^H \pi x^2dy=\dfrac{\pi v^2}{g}\int_{0}^H2h+\dfrac{v^2}{g}-2ydy=\dfrac{2\pi v^2}{g}\int_{0}^HH-ydy \\
&=\dfrac{\pi v^2}{g}\cdot H^2=\dfrac{\pi v^2}{g}\cdot(h+\dfrac{v^2}{2g})^2
\end{aligned}$$

## 代码

```py
from math import pi

h = 100
v = 20
g = 9.81
ans = pi * (2 * g * v * h + v ** 3) ** 2 / (4 * g ** 3)
print("{:.4f}".format(ans))

```
