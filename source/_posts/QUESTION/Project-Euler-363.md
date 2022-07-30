---
title: Project Euler 363
tags:
  - Project Euler
mathjax: true
date: 2022-07-27 23:50:38
---

<escape><!-- more --></escape>

# Project Euler 363

## 题目

### Bézier Curves

A cubic Bézier curve is defined by four points: $P_0, P_1, P_2,$ and $P_3$.

![](../images/p363_bezier.png)

The curve is constructed as follows:

On the segments $P_0 P_1$, $P_1 P_2$, and $P_2 P_3$ the points $Q_0, Q_1,$ and $Q_2$ are drawn such that $\dfrac{P_0 Q_0}{P_0 P_1} = \dfrac{P_1 Q_1}{P_1 P_2} = \dfrac{P_2 Q_2}{P_2 P_3} = t$, with $t$ in $[0, 1]$.

On the segments $Q_0 Q_1$ and $Q_1 Q_2$ the points $R_0$ and $R_1$ are drawn such that

$\dfrac{Q_0 R_0}{Q_0 Q_1} = \dfrac{Q_1 R_1}{Q_1 Q_2} = t$ for the same value of $t$.

On the segment $R_0 R_1$ the point $B$ is drawn such that $\dfrac{R_0 B}{R_0 R_1} = t$ for the same value of $t$.

The Bézier curve defined by the points $P_0, P_1, P_2, P_3$ is the locus of $B$ as $Q_0$ takes all possible positions on the segment $P_0 P_1$.
(Please note that for all points the value of $t$ is the same.)

From the construction it is clear that the Bézier curve will be tangent to the segments $P_0 P_1$ in $P_0$ and $P_2 P_3$ in $P_3$.

A cubic Bézier curve with $P_0 = (1, 0), P_1 = (1, v), P_2 = (v, 1),$ and $P_3 = (0, 1)$ is used to approximate a quarter circle.

The value $v \gt 0$ is chosen such that the area enclosed by the lines $O P_0, OP_3$ and the curve is equal to $\dfrac{\pi}{4}$ (the area of the quarter circle).

By how many percent does the length of the curve differ from the length of the quarter circle?

That is, if $L$ is the length of the curve, calculate $100 \times \dfrac{L - \frac{\pi}{2}}{\frac{\pi}{2}}$

Give your answer rounded to $10$ digits behind the decimal point.

## 解决方案

这个[页面](https://en.wikipedia.org/wiki/B%C3%A9zier_curve#Cubic_B%C3%A9zier_curves)给出了这条三次贝塞尔曲线的参数方程：

$${\displaystyle \mathbf {B} (t)=\mathbf {P} _{0}(1-t)^{3}+3\mathbf {P} _{1}t(1-t)^{2}+3\mathbf {P} _{2}t^{2}(1-t)+\mathbf {P} _{3}t^{3}{,}t\in [0,1]}$$

那么化简后，得到关于$x,y$的参数方程：

$$\begin{aligned}
x(t)&=(1-t)^3+3t(1-t)^2+3t^2(1-t)v\\
y(t)&=3t(1-t)^2v+3t^2(1-t)+t^3
\end{aligned}$$

第一个问题：如何求贝塞尔曲线$B$和线段$C:P_3O,D:OP_0)$**共同**围绕而成的封闭曲线的面积？

使用补线法进行计算，可以列出公式为：

$$\dfrac{\pi}{4}=S=\dfrac{1}{2}\int_{B+C+D}xdy-ydx$$

注意线段$B$和线段$C$的积分值都为$0$，那么只需要计算$\dfrac{1}{2}\int_Bxdy-ydx$即可。

$$\dfrac{1}{2}(1+\dfrac{6v}{5}-\dfrac{3v^2}{10})=\dfrac{\pi}{4}$$

解这个一元二次方程，得到$v=2\pm\sqrt{\dfrac{1}{3}(22-5\pi)}$。

由于按照题目的需要，它是一个$\dfrac{1}{4}$圆的近似，因此取$v=2-\sqrt{\dfrac{1}{3}(22-5\pi)}$

第二个问题：如何求曲线的长度？

$$d_{P_0P_3}=\int_0^1\sqrt{x'^2(t)+y'^2(t)}dt$$

通过Mathematica直接计算出具体值即可。

## 代码

```Mathematica
x[t_] = (1 - t)^3 + 3 t (1 - t)^2 + 3 t^2 (1 - t) v
y[t_] = 3 t (1 - t)^2 v + 3 t^2 (1 - t) + t^3
sol = First[Solve[1/2 (Integrate[x[t] y'[t] - y[t] x'[t], {t, 0, 1}]) == Pi/4, v]]
L = NIntegrate[Sqrt[x'[t]^2 + y'[t]^2 /. sol], {t, 0, 1}]
ans = 100*(L - Pi/2)/(Pi/2)
```
