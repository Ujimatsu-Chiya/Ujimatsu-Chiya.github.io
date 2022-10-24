---
title: Project Euler 321
category:
  - Project Euler
tags:
  - 佩尔方程
mathjax: true
date: 2022-06-02 21:03:34
---

<escape><!-- more --></escape>

# Project Euler 321

## 题目

### Swapping Counters

A horizontal row comprising of $2n + 1$ squares has $n$ red counters placed at one end and $n$ blue counters at the other end, being separated by a single empty square in the centre. For example, when $n = 3$.

![](../images/p321_swapping_counters_1.gif)

A counter can move from one square to the next (slide) or can jump over another counter (hop) as long as the square next to that counter is unoccupied.

![](../images/p321_swapping_counters_2.gif)

Let $M(n)$ represent the minimum number of moves/actions to completely reverse the positions of the coloured counters; that is, move all the red counters to the right and all the blue counters to the left.

It can be verified $M(3) = 15$, which also happens to be a triangle number.

If we create a sequence based on the values of n for which $M(n)$ is a triangle number then the first five terms would be: $1, 3, 10, 22,$ and $63$, and their sum would be $99$.

Find the sum of the first forty terms of this sequence.

## 解决方案

第一个问题：$M(n)$的式子是什么？

可以发现，每一枚筹码如果移动到它的目标格子，都需要前进$n+1$格，因此$2n$枚筹码就总共需要前进$2n(n+1)$格子。

但是，当两个不同颜色的筹码相遇时，一个筹码就可以朝另一个筹码跳跃，一次操作就会前进$2$格格子。这样的相遇一共会发生$n^2$次。

因此，$M(n)=2n(n+1)-n^2=n^2+2n$。

第二个问题：求解问题中要求的数。

如果$M(n)$为三角数，设存在m，使得$n^2+2n=\dfrac{m(m+1)}{2}$。

移项，两边同乘一个数$8$，得到$4m(m+1)-8(n^2+2n)=0$

进行配方，移项后得到$(2m+1)^2-8(n+1)^2=-7$。

令$x=2m+1,y=n+1$，那么得到$x^2-8y^2=-7$，该类方程为[广义佩尔方程](https://en.wikipedia.org/wiki/Pell%27s_equation#Generalized_Pell's_equation)：$x^2-Dy^2=N$。

但是，广义佩尔方程的基础解有多个，不像$N=1,-1$时的情形。

经过一定范围的搜索，发现这个方程有$6$个基本解：

$(1, 1), (5, 2)$

使用与第137题类似的方法，每一组$x^2-8y^2=-7$的通解由它的一个基础解$(x_1,y_1)$和$x^2-8y^2=1$的通解$(a_k,b_k)$得到。

$$\left \{\begin{aligned}
  & x_{k+1}=x_1a_k+Dy_1b_k\\
  & y_{k+1}=y_1a_k+x_1b_k
\end{aligned}\right.
$$

再根据第66题的算法，可以得到$x^2-8y^2=1$的通解：
$$a_1=3,b_1=1$$
$$\left \{\begin{aligned}
  & a_{k+1}=3a_k+8b_k\\
  & b_{k+1}=a_k+3b_k
\end{aligned}\right.
$$

计算出每一对$(x,y)$后，需要回代$m=\dfrac{x-1}{2},n=y-1$。判断这时$m,n$是否为正整数。最终求出这些$n$的和

## 代码

```py
N = 40


def gen_solution():
    D = 8
    base_sol = [(1, 1), (5, 2)]
    a, b = 3, 1
    for x, y in base_sol:
        yield x, y
    while True:
        for i in range(len(base_sol)):
            x, y = base_sol[i]
            x, y = x * a + D * y * b, x * b + y * a
            yield x, y
        a, b = 3 * a + 8 * b, a + 3 * b


ls = []
for x, y in gen_solution():
    if (x - 1) % 2 == 0 and (x - 1) // 2 > 0:
        ls.append(y - 1)
        if len(ls) == N:
            break
ans = sum(ls)
print(ans)

```
