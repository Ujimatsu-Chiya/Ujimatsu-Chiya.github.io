---
title: Project Euler 493
tags:
  - Project Euler
  - 概率
mathjax: true
date: 2022-06-05 09:28:48
---

<escape><!-- more --></escape>

# Project Euler 493

## 题目

### Under The Rainbow

$70$ colored balls are placed in an urn, $10$ for each of the seven rainbow colors.

What is the expected number of distinct colors in $20$ randomly picked balls?

Give your answer with nine digits after the decimal point (a.bcdefghij).

## 解决方案

假设每一组有$m=10$个球，一共有$g=7$组，一次取出$p=20$个球。

令$X_i$表示第$i$种颜色的球出现的示性随机变量。如果$X_i=1$，那么就说明第$i$种颜色出现了，如果$X_i$为$0$，那么第$i$种颜色没有出现。

那么，最终出现颜色个数的期望为

$$e=E[\sum_{i=1}^gX_i]=\sum_{i=1}^gE[X_i]$$

不失一般性，对于第$1$种颜色的球，它被抽出来的概率为$1-\dfrac{C_{m(g-1)}^p}{C_{mg}^p}$。

因此，$E[X_1]=1-\dfrac{C_{m(g-1)}^p}{C_{mg}^p}$

由于所有颜色的球的数量都是一样的，因此$E[X_1]=E[X_2]=\dots=E[X_g]$。

因此最终答案为

$$e=\sum_{i=1}^gE[X_i]=gE[X_1]=g(1-\dfrac{C_{m(g-1)}^p}{C_{mg}^p})$$

## 代码

```py
from tools import C

M = 10
G = 7
P = 20
N = M * G

ans = G * (1 - C(N - M, P) / C(N, P))
print("{:.9f}".format(ans))

```
