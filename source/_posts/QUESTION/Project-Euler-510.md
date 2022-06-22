---
title: Project Euler 510
tags:
  - Project Euler
mathjax: true
date: 2022-06-22 23:27:05
---

<escape><!-- more --></escape>

# Project Euler 510

## 题目

### Tangent Circles

Circles $A$ and $B$ are tangent to each other and to line $L$ at three distinct points.

Circle $C$ is inside the space between $A, B$ and $L$, and tangent to all three.

Let $r_A, r_B$ and $r_C$ be the radii of A, B and C respectively.

![](../images/p510_tangent_circles.png)

Let $S(n)=\sum r_A+r_B+r_C$, for $0<r_A\le r_B\le n$ where $r_A, r_B$ and $r_C$ are integers.

The only solution for $0<r_A\le r_B\le5$ is $r_A=4, r_B=4$ and $r_C=1$, so $S(5)=4+4+1=9$.

You are also given $S(100)=3072$.

Find $S(10^9)$.

## 笛卡尔定理

[笛卡尔定理](https://en.wikipedia.org/wiki/Descartes%27_theorem#Special_cases)的一种特殊情况：假设三个圆$A,B,C$两两相切，它们的半径分别是$r_A,r_B,r_C$，并且存在一条直线$L$，使得$L$是这三个圆的公切线。如果圆$C$在$L$上的切点位于另外两个圆$A,B$的切点的中间，那么$r_A,r_B,r_C$满足此式子：

$$\dfrac{1}{\sqrt{r_A}}+\dfrac{1}{\sqrt{r_B}}=\dfrac{1}{\sqrt{r_C}}$$

在这个特殊情况下，原本笛卡尔定理中的第四个圆的曲率被认为是$0$。

## 解决方案

可以将上面的式子写成

$$r_C=\dfrac{r_Ar_B}{r_A+r_B+2\sqrt{r_Ar_B}}$$

不难看出，如果$r_C$是一个有理数，那么$r_Ar_B$必须是一个平方数。

假设$r_A=ta^2,r_B=tb^2,a\le b,\gcd(a,b)=1,t>0$，那么就可以将$(r_A,r_B,r_C)$写成一个三元组形式$(ta^2,tb^2,\dfrac{ta^2b^2}{(a+b)^2})$

因此，$(a+b)^2|t$。

那么，重新令$r_A=dp^2(p+q)^2,r_B=dq^2(p+q)^2,r_C=dp^2q^2$，其中$p\le q,\gcd(p,q)=1,d>0$，那么枚举出每对互质的$(p,q)$和$d$，就产生了一对符合要求的三元组$(r_A,r_b,r_C)$。

在代码实现中，$(p,q)$的枚举是在[Stern-Brocot Tree](https://en.wikipedia.org/wiki/Stern%E2%80%93Brocot_tree)上进行。

## 代码

```py
N = 10 ** 9


def cal(p, q):
    a, b, c = p ** 2 * (p + q) ** 2, q ** 2 * (p + q) ** 2, (p * q) ** 2
    d = N // b
    return d * (d + 1) // 2 * (a + b + c)


ans = cal(1, 1)
st = [(0, 1, 1, 1)]
while len(st) > 0:
    a, c, b, d = st.pop()
    p, q = a + b, c + d
    w = cal(p, q)
    if w > 0:
        ans += w
        st.append((a, c, p, q))
        st.append((p, q, b, d))
print(ans)

```
