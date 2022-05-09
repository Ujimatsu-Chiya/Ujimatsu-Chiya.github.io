---
title: Project Euler 140
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 140

## 题目

### Modified Fibonacci golden nuggets

Consider the infinite polynomial series $A_G(x) = x G_1 + x^2 G_2 + x^3 G_3 + \cdots$, where $G_k$ is the $k$th term of the second order recurrence relation $G_k = G_{k-1} + G_{k-2}$, $G_1 = 1$ and $G_2 = 4$; that is, $1, 4, 5, 9, 14, 23, \dots$ .

For this problem we shall be concerned with values of $x$ for which $A_G(x)$ is a positive integer.

The corresponding values of $x$ for the first five natural numbers are shown below.

|$x$|$A_G(x)$|
|-|-|
|$\dfrac{\sqrt{5}-1}{4}$|$1$|
|$\dfrac{2}{5}$|$2$|
|$\dfrac{\sqrt{22}-2}{6}$|$3$|
|$\dfrac{\sqrt{137}-5}{14}$|$4$|
|$\dfrac{1}{2}$|$5$|

We shall call $A_G(x)$ a golden nugget if $x$ is rational, because they become increasingly rarer; for example, the 20th golden nugget is $211345365$.

Find the sum of the first thirty golden nuggets.

## 解决方案

和137题一样，有

$$
\begin{aligned}
A_G(x)      & =xG_1+    & x^2G_2+x^3G_3+\dots \\
xA_G(x)     & =         & x^2G_1+x^3G_2+\dots\\
(1+x)A_G(x) &=xG_1+ &x^2G_3+x^3G_4+\dots\\
\end{aligned}
$$

可以发现，第三条式子用了定义：$G_n=G_n-1+G_n-2$。

将$A_F(x)$代入第三条式子右侧，有：

$$
(1+x)A_G(x)=xG_1+\dfrac{A_G(x)}{x}-G_1-xG_2
$$

代入$G_1=1,G_2=4$，化简后，有：

$$A_G(x)=\dfrac{3x^2+x}{1-x-x^2}$$

令$A_F(x)=n$，$n$是一个正整数，有：$3x^2+x=n(1-x-x^2)$

化成关于$x$的一元二次方程，有$(n+3)x^2+(n+1)x-n=0$

如果$x$是一个有理数，那么其判别式$\Delta$必须是有理数。也就是$(n+1)^2-4n^2=5n^2+2n+1$必须是一个平方数。

如果方程的解$x$是一个有理数，那么其判别式$\Delta$必须是有理数。也就是$(n+1)^2+4n(n+3)=5n^2+14n+1$必须是一个平方数。

因此，令正整数$y$满足$y^2=5n^2+14n+1$。

两边同乘$5$，并配方，得$25n^2+70n+49-44=m^2$

移项，得：$(5n+7)^2-5y^2=44$

令$x=5n+7$，那么得到$x^2-5y^2=44$。这种广义佩尔方程和137题不同的是，后面的$N$变成$44$了。

经过一定范围的搜索，发现这个方程有$6$个基本解：

$(7,1),(8,2),(13,5),(17,7),(32,14),(43,19)$

使用与137题类似的方法，每一组通解$x^2-5y^2=44$的由一个基础解$(x_1,y_1)$和$x^2-5y^2=1$的通解$(a_k,b_k)$得到。

$$\left \{\begin{aligned}
  & x_{k+1}=x_1a_k+Dy_1b_k\\
  & y_{k+1}=y_1a_k+x_1b_k
\end{aligned}\right.
$$

将求出的$x$回代$n=\dfrac{x-7}{5}$。第$15$小的正整数$n$为所求。

## 代码

```py
N = 30


def gen_solution():
    D = 5
    base_sol = [(7, 1), (8, 2), (13, 5), (17, 7), (32, 14), (43, 19)]
    a, b = 9, 4
    for x, y in base_sol:
        yield x
    while True:
        for i in range(len(base_sol)):
            x, y = base_sol[i]
            x, y = x * a + D * y * b, x * b + y * a
            yield x
        a, b = 9 * a + 20 * b, 4 * a + 9 * b


ls = []
for x in gen_solution():
    if (x - 7) % 5 == 0:
        w = (x - 7) // 5
        if w > 0:
            ls.append((x - 7) // 5)
    if len(ls) == N:
        break

ans = sum(ls)
print(ans)

```
