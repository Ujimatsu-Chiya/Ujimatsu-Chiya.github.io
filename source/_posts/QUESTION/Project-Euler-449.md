---
title: Project Euler 449
date: 2022-04-12 18:33:54
tags: 
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 449

## 题目

### Chocolate covered candy

Phil the confectioner is making a new batch of chocolate covered candy. Each candy centre is shaped like an ellipsoid of revolution defined by the equation: $b^2x^2 + b^2y^2 + a^2z^2 = a^2b^2$.

Phil wants to know how much chocolate is needed to cover one candy centre with a uniform coat of chocolate one millimeter thick.

If $a=1\mathrm{mm}$  and $a=1\mathrm{mm}$, the amount of chocolate required is $\frac{28}{3}π \mathrm{mm^3}$.

If $a=2\mathrm{mm}$  and $a=1\mathrm{mm}$, the amount of chocolate required is approximately $60.35475635 \mathrm{mm^3}$.

Find the amount of chocolate in $\mathrm{mm^3}$ required if $a=3 \mathrm{mm}$ and $b=1 \mathrm{mm}$. Give your answer as the number rounded to $8$ decimal places behind the decimal point.

## 平行曲线(Parallel Curves)

[平行曲线](https://mathworld.wolfram.com/ParallelCurves.html)，即将这个曲线上的所有点朝着其在曲线上的法线方向移动相同的距离。可以向内也可以向外。

如果一个曲线$F$的参数方程为$(f(t),g(t))$，移动$k$的距离，那么移动后的曲线$F'$的参数方程为
$$\left\{
\begin{aligned}
x(t) & = & f(t)\pm\frac{kg'(t)}{\sqrt{f'^2(t)+g'^2(t)}} \\
y(t) & = & g(t)\mp\frac{kf'(t)}{\sqrt{f'^2(t)+g'^2(t)}}
\end{aligned}
\right.
$$

## 解决方案

本题中可将椭圆的方程化为$\frac{x^2}{a^2}+\frac{y^2}{a^2}+\frac{z^2}{b^2}=1$.因此可以将这个物体视为是$XOZ$平面上一个围绕$z$轴的旋转体。

那么，$XOZ$平面上的这个方程可以视为$\frac{x^2}{a^2}+\frac{z^2}{b^2}=1$.

那么可以看出，这个$XOZ$平面上的椭圆的参数方程为$x=a\cos t,z=b\sin t$.

本体题意所需要的新的平行曲线是向外的，因此代入平行曲线中的式子，可以得到

$$\left\{
\begin{aligned}
x(t) & = & a\cos t + \frac{bk \cos t}{\sqrt{a^2\sin ^2t+b^2 \cos^2 t}} \\
z(t) & = & b\sin t + \frac{ak \sin t}{\sqrt{a^2\sin ^2t+b^2 \cos^2 t}}
\end{aligned}
\right.
$$
那么最终形成的物体的体积为
$$V=\int _{-\frac{\pi}{2}}^{\frac{\pi}{2}}\pi x^2(t) d(z(t))=\int_{-\frac{\pi}{2}}^{\frac{\pi}{2}}\pi x^2(t) z'(t)dt$$

减去原来已经有的，那么答案为$V_0=V-\frac{4}{3}\pi a^2b$。

## 代码

```Mathematica
a = 3
b = 1
k = 1
x[t_] = a Cos[t] + b k Cos[t]/Sqrt[(a Sin[t])^2 + (b Cos[t])^2]
z[t_] = b Sin[t] + a k Sin[t]/Sqrt[(a Sin[t])^2 + (b Cos[t])^2]
N[Integrate[Pi*x[t]^2*D[z[t], t], {t, -Pi/2, Pi/2}] - 4 Pi a^2 b/3, 11]
```
