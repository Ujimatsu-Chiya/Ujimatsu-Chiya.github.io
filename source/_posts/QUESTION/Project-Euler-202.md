---
title: Project Euler 202
tags:
  - Project Euler
mathjax: true
date: 2022-07-01 17:36:59
---

<escape><!-- more --></escape>

# Project Euler 202

## 题目

### Laserbeam

Three mirrors are arranged in the shape of an equilateral triangle, with their reflective surfaces pointing inwards. There is an infinitesimal gap at each vertex of the triangle through which a laser beam may pass.

Label the vertices $A, B$ and $C$. There are $2$ ways in which a laser beam may enter vertex $C$, bounce off $11$ surfaces, then exit through the same vertex: one way is shown below; the other is the reverse of that.

![](../images/p201_laserbeam.gif)

There are $80840$ ways in which a laser beam may enter vertex $C$, bounce off $1000001$ surfaces, then exit through the same vertex.

In how many ways can a laser beam enter at vertex $C$, bounce off $12017639147$ surfaces, then exit through the same vertex?

## 莫比乌斯反演

[莫比乌斯反演](https://en.wikipedia.org/wiki/M%C3%B6bius_inversion_formula)：假设有两个算术函数$f,g$，其中$f$可以写成$g$的以下关系式：

$$g(n)=\sum_{d|n}f(d)$$

那么有

$$f(n)=\sum_{d|n}\mu(\dfrac{n}{d})g(d)$$

其中$\mu$是莫比乌斯函数。

注意算术函数$f$可以看成是$g$和$\mu$的[狄利克雷卷积](https://en.wikipedia.org/wiki/Dirichlet_convolution)，可以记作$f=\mu*g$.

## 解决方案

令$N=12017639147$。处理光线反射问题，最常使用的方法是将整个图形按照镜面对称地拓展开来。这时，处理反射的问题就变成了处理直线的问题。

我们对这个等边三角形进行拓展，得到下图：

![](../images/p202-2.png)

其中，蓝色点就是通过镜面拓展出来后的$C$点。

由于这是一个三角形阵列，不容易对每个点进行坐标编排，因此以原图中的点$C$为原点，将整个三角形阵列转化为平面直角坐标系上的点，如下图：

![](../images/p202-3.png)

那么很容易地观察出，拓展出来的$C(x,y)$满足关系：$y\equiv x(\mod 3)$。

如果光线不会提前射出，那么说明这个光线在经过拓展出来的点之前，是不会经过其它**格点**的。也就是说，$\gcd(x,y)=1$。

另一个观察：如果光线射到一个格点$(x,y)$，那么它实际上被镜子反射$(x-1)+(y-1)+(x+y-1)=2x+2y-3$次。因为他经过了$y-1$条水平的线（镜子），$x-1$条垂直的线，以及$x+y-1$条形如$x+y=k$的直线。

也就是说，如果一个点$(x,y)$满足$x+y=n,\gcd(x,y)=1$，那么光线射到这个点时已经反射了$2n-3$次，注意到$2n-3$一定是一个奇数。

那么很明显，当$N$为偶数时，答案为$0$。当$M=\dfrac{N+3}{2}$为$3$的倍数时，答案也为$0$，因为$x+y=3k$上的所有$C$点的横纵坐标的最小公因数为$3$，不合题意。

在上面的图中，当$n$不为$3$的倍数时，很容易数出直线$x+y=n$上有$F(n)=\dfrac{n-G(n)}{3}$个点是$C$点，其中$G(n)\in\{-1,1\},G(n)\equiv n(\mod 3)$。

假设$f(n)$是在直线$x+y=n$上那些能被原点“看见”（也就是$\gcd(x,y)=1$）的$C$点个数，那么$x+y=n$上被挡住的那些$C(x,y)$点将会被点$C'(\dfrac{x}{d},\dfrac{y}{d})$挡住，其中$d=\gcd(x,y)$。注意到$C'$落在直线$x+y=\dfrac{n}{d}$上，并且$\dfrac{n}{d}$是$n$的一个因子。那么可以写出下面关于两个函数$F$和$f$的式子：

$$F(n)=\sum_{d|n}f(d)$$

根据莫比乌斯反演，$f$可以写成如下形式：

$$\begin{aligned}
f(n)&=\sum_{d|n}\mu(\dfrac{n}{d})\cdot F(n)\\
&=\dfrac{1}{3}(\sum_{d|n}\mu(\dfrac{n}{d})\cdot d-\sum_{d|n}\mu(\dfrac{n}{d})\cdot G(d))\\
\end{aligned}$$

在狄利克雷卷积的页面中，发现$\varphi=\mu*\text{Id}$，其中$\text{Id}(n)=n$，$\varphi$为欧拉函数。

令$g(n)=\sum_{d|n}\mu(\dfrac{n}{d})\cdot G(d)=\sum_{d|n}\mu(\dfrac{n}{d})\cdot G(n)\cdot G(\dfrac{n}{d})=G(n)\sum_{d|n}\mu(d)\cdot G(d)$.

考虑上面求和式$g(n)$的值，但是这里只考虑因数$d$满足$\mu(d)\neq 0$的情况，注意此时$d$是一个无平方因子数。

1. 当$n$包含模$3$余$1$的质因子$p$时，那么$g(n)=0$。假设$p\nmid d$，那么发现$\mu(d)=-\mu(pd)$，但是$G(d)=G(pd)$，那么有$\mu(d)\cdot G(d)+\mu(pd)\cdot G(pd)=0$。最终将这样的一对对$p,d$值的式子相加，即可得到$g(n)=0$。

2. 当$n$不包含模$3$余$1$的质因子时，那么$g(n)=G(n)\cdot 2^r$，其中$r$是$n$的**不同**质因子个数。因为$\mu(d)$必定和$G(d)$是同号的，即$\mu(d)\cdot G(d)=1$。$r$个不同的质因子意味着$n$有$2^r$个无平方因子，故得上式。

因此，本题先计算出$M$，然后计算出$f(M)=\dfrac{1}{3}(\varphi(M)-g(M))$即可。

## 代码

```py
from tools import phi, factorization

N = 12017639147


def cal(n):
    if n % 2 == 0:
        return 0
    m = (n + 3) // 2
    if m % 2 == 0:
        return 0
    ls = factorization(m)
    s = phi(m)
    if 1 not in [a[0] for a in ls]:
        g = -1 if m % 3 == 2 else 1
        s -= g * 2 ** len(ls)
    return s // 3


ans = cal(N)
print(ans)

```
