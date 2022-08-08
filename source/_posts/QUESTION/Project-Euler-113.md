---
title: Project Euler 113
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-05-06 22:24:05
---

<escape><!-- more --></escape>

# Project Euler 113

## 题目

### Non-bouncy numbers

Working from left-to-right if no digit is exceeded by the digit to its left it is called an increasing number; for example, $134468$.

Similarly if no digit is exceeded by the digit to its right it is called a decreasing number; for example, $66420$.

We shall call a positive integer that is neither increasing nor decreasing a "bouncy" number; for example, $155349$.

As $n$ increases, the proportion of bouncy numbers below n increases such that there are only $12951$ numbers below one-million that are not bouncy and only $277032$ non-bouncy numbers below $10^{10}$.

How many numbers below a googol ($10^{100}$) are not bouncy?

## 解决方案

所谓的上升数和下降数，下一位的值只能都大于等于上一位或者小于等于上一位。因此可以用动态规划的方法统计$n$位数的上升数和下降数。

分别设两个状态$f(i,d),g(i,d)(1\le i\le n,0\le d\le 9)$表示$i$位数中，个位为$d$的上升数/下降数分别有多少个。

注意到上升数的每一位中，下一位的值只能都大于等于上一位，可以列出$f(i,j)$的状态转移方程：

$$
f(i,d)=
\left \{\begin{aligned}
  &0  & & \mathrm{if\quad} i=1\& d=0 \\
  &1  & & \mathrm{else if\quad} i=1 \\
  &\sum_{j=0}^d f(i-1,j) & & \mathrm{else}
\end{aligned}\right.
$$

类似的，可以列出$g(i,j)$的状态转移方程：

$$
g(i,d)=
\left \{\begin{aligned}
  &0  & & \mathrm{if\quad} i=1\& d=0 \\
  &1  & & \mathrm{else if\quad} i=1 \\
  &\sum_{j=d}^9 g(i-1,j) & & \mathrm{else}
\end{aligned}\right.
$$

注意到，$111\dots111,222\dots222$这种$n$位都是一样的数都算进了上升数和下降数中，因此最终答案需要减去这两种数多算的一次。

最终答案为：

$$\sum_{i=1}^n\sum_{d=0}^9(f(i,d)+g(i,d)-1)$$

## 代码

```py
N = 100
f = [1 for _ in range(10)]
f[0] = 0
g = f.copy()
ans = 9
for i in range(N - 1):
    f = [sum(f[:i + 1]) for i in range(10)]
    g = [sum(g[i:]) for i in range(10)]
    ans += sum(f) + sum(g) - 9
print(ans)

```
