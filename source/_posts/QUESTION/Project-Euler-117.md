---
title: Project Euler 117
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-05-06 22:24:21
---

<escape><!-- more --></escape>

# Project Euler 117

## 题目

### Red, green, and blue tiles

Using a combination of grey square tiles and oblong tiles chosen from: red tiles (measuring two units), green tiles (measuring three units), and blue tiles (measuring four units), it is possible to tile a row measuring five units in length in exactly fifteen different ways.

![](../images/p117.png)

How many ways can a row measuring fifty units in length be tiled?

NOTE: This is related to <a href="/Problem101-125/#Problem_116">Problem 116</a>.

## 解决方案

与第116题不同，这里的砖块是可以随便使用的，没有任何限制。

假设铺成的长度为$n=50$。设$f(i)(0\leq i\leq n)$为铺设成长度为$i$的方案数量，那么可以列出以下状态转移方程：

$$
f(i)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=0, 1 \\
  &2  & & \mathrm{else if\quad} i=2\\
  &4  & & \mathrm{else if\quad} i=3 \\
  &f(i-1)+f(i-2)+f(i-3)+f(1-4) & & \mathrm{else}
\end{aligned}\right.
$$

方程的最后一行表示：所有$f(i-1)$的方案后面多拼接一个黑色方块；同理，$f(i-2),f(i-3),f(i-4)$则对应后面接一个红色，绿色，蓝色。

初值$f(1),f(2),f(3)$的产生：在这些长度下，如果套用第四条式子，会发生$f$自变量小于$0$的情况，这里我们就选择忽略掉这些小于$0$的转移情况。也就是说，当$i<0$时，可以认为$f(i)=0$。

## 代码

本代码适用于填充的方块为任意种类任意长度的情况。

```py
N = 50
M = [1, 2, 3, 4]
f = [1]
for i in range(1, N + 1):
    f.append(sum((0 if i < k else f[i - k]) for k in M))
ans = f[N]
print(ans)

```

本代码则仅适用于本题。

```py
N = 50
f = [1, 1, 2, 4]
for i in range(4, N + 1):
    f.append(f[-1] + f[-2] + f[-3] + f[-4])
print(f[N])

```
