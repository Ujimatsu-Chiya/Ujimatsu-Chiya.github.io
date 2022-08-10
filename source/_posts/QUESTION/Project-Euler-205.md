---
title: Project Euler 205
category:
  - Project Euler
tags:
  - 概率
  - 动态规划
mathjax: true
date: 2022-05-30 20:28:12
---

<escape><!-- more --></escape>

# Project Euler 205

## 题目

### Dice Game

Peter has nine four-sided (pyramidal) dice, each with faces numbered $1, 2, 3, 4$.
Colin has six six-sided (cubic) dice, each with faces numbered $1, 2, 3, 4, 5, 6$.

Peter and Colin roll their dice and compare totals: the highest total wins. The result is a draw if the totals are equal.

What is the probability that Pyramidal Pete beats Cubic Colin? Give your answer rounded to seven decimal places in the form 0.abcdefg

## 解决方案

为了求出Peter击败Colin的概率是多少，需要知道各自投出的点数和的分布律。

假设某一人有$c$个骰子，这个骰子有$n$面，考虑使用动态规划的思想用来计算这个分布和：令$f_{c,n}(i,j)(0\le i\le c,0\le j\le cn)$表示使用了$i$个骰子时，投掷出和为$j$概率，那么不难列出如下状态转移方程：

$$
f_{c,n}(i,j)=
\left \{\begin{aligned}
  &1  & & \text{if\quad} i=0\land j=0 \\
  &0 & & \text{else if\quad} i=0\lor j=0 \\
  &\sum_{k=1}^{\min(j,n)}\dfrac{f_{c,n}(i-1,j-k)}{n} & & \text{else}
\end{aligned}\right.
$$

对于方程的第三行，状态$f_{c,n}(i-1,j-k)$都有$\dfrac{1}{n}$的概率转移到当前状态。

最终，所求的分布律为$f_{c,n}(c,\cdot)$。

假设Peter的分布律是$f(\cdot)=f_{c_P,n_P}(c_P,\cdot)$，Colin的分布律为$g(\cdot)=f_{c_C,n_C}(c_C,\cdot)$。那么，Peter击败Colin的概率为：

$$\sum_{i=1}^{c_P\cdot n_P}\sum_{j=0}^{\min(i-1,c_C\cdot n_C)}f(i)\cdot g(j)$$

## 代码

```py
CP, NP = 9, 4
CC, NC = 6, 6


def get_distribution(c: int, n: int):
    f = [[0 for _ in range(c * n + 1)] for _ in range(c + 1)]
    f[0][0] = 1
    for i in range(1, c + 1):
        for j in range(c * n + 1):
            for k in range(1, min(j, n) + 1):
                f[i][j] += f[i - 1][j - k] / n
    return f[c]


distribute_p = get_distribution(CP, NP)
distribute_c = get_distribution(CC, NC)
ans = s = 0
for i in range(1, len(distribute_p)):
    ans += distribute_p[i] * sum(distribute_c[:i])
print("{:.7f}".format(ans))

```
