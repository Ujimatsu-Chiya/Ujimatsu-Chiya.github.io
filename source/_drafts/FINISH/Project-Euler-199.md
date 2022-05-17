---
title: Project Euler 199
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 199

## 题目

### Iterative Circle Packing

Three circles of equal radius are placed inside a larger circle such that each pair of circles is tangent to one another and the inner circles do not overlap. There are four uncovered “gaps” which are to be filled iteratively with more tangent circles.

![](../images/p199_circles_in_circles.gif)

At each iteration, a maximally sized circle is placed in each gap, which creates more gaps for the next iteration. After $3$ iterations (pictured), there are $108$ gaps and the fraction of the area which is not covered by circles is $0.06790342$, rounded to eight decimal places.

What fraction of the area is not covered by circles after $10$ iterations?

Give your answer rounded to eight decimal places using the format x.xxxxxxxx .
# 笛卡尔定理

### 曲率
如果一个圆的半径为$r$，那么其曲率$k$满足$|k|=\dfrac{1}{r}$。对于两个圆而言，如果两个圆外切，那么曲率的正负符号相同；如果为内切，那么符号不同。

[笛卡尔定理](https://en.wikipedia.org/wiki/Descartes%27_theorem)：假设$4$个两两相切的圆的曲率分别为$k_1,k_2,k_3,k_4$，且这四个圆两两相切的切点均不同。那么这四个圆的曲率满足：

$$(k_1+k_2+k_3+k_4)^2=2(k_1^2+k_2^2+k_3^2+k_4^2)$$

如果已知三个圆的曲率，那么第四圆的曲率可以写成：

$$k_4=k_1+k_2+k_3\pm2\sqrt{k_1k_2+k_2k_3+k_3k_1}$$

## 解决方案

为了避免重复计算，可以先将相同面积的合并计算。

递归遍历所有的小圆，用笛卡尔定理计算它们的面积。

计算第$4$个圆的曲率时，上面的公式取正号，是因为目前所求的所有圆都是和参数中的正曲率两个圆外切（只有外面那个大圆是负曲率的）。

## 代码

```py
N = 10


def getS(r: float):
    return r * r


def dfs(k1: float, k2: float, k3: float, d: int):
    k4 = k1 + k2 + k3 + 2 * (k1 * k2 + k2 * k3 + k3 * k1) ** 0.5
    ans = getS(1 / k4)
    if d == 1:
        return ans
    return ans + dfs(k1, k2, k4, d - 1) + dfs(k1, k3, k4, d - 1) + dfs(k2, k3, k4, d - 1)


inK = inR = 1
# 三个小圆内切于大圆，故大圆曲率为负。
outK = 3 - 2 * 3 ** 0.5
outR = -1 / outK
ans = getS(inR) * 3 + dfs(inK, inK, outK, N) * 3 + dfs(inK, inK, inK, N)
ans = 1 - ans / getS(outR)
print("{:.8f}".format(ans))

```