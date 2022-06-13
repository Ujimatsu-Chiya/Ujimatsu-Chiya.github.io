---
title: Project Euler 228
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 228
## 题目
### Minkowski Sums

Let $S_n$ be the regular $n$-sided polygon – or *shape* – whose vertices $v_k (k=1,2,\dots,n)$ have coordinates:

$$x_k= \cos(\dfrac{2k-1}{n} \times 180°)\quad y_k= \sin(\dfrac{2k-1}{n} \times 180°)$$

Each $S_n$ is to be interpreted as a filled shape consisting of all points on the perimeter and in the interior.

The *Minkowski sum*, $S+T$, of two shapes $S$ and $T$ is the result of adding every point in $S$ to every point in $T$, where point addition is performed coordinate-wise: $(u,v) + (x,y) = (u+x,v+y)$.

For example, the sum of $S_3$ and $S_4$ is the six-sided shape shown in pink below:

![](../images/p228.png)

How many sides does $S_{1864}+S_{1865}+\dots+S_{1909}$ have?


## 解决方案

这个[页面](https://en.wikipedia.org/wiki/Minkowski_addition#Two_convex_polygons_in_the_plane)描述了求两个**凸包**$P,Q$的闵可夫斯基和的方法：

1. 分别逆时针沿着两个正$n$多边形$P,Q$的边界行走，枚举出$n$个边界的向量（如下图所示）。

2. 将这些向量按照**极角**进行排序。

3. 按顺序将这些向量首尾拼接，那么拼接出来的必定是一个封闭图形。这个图形就是$P,Q$的闵可夫斯基和。

回到题目中，在求闵可夫斯基和的第三个步骤中，如果两个向量的极角相同，那么说明构造出来的新凸包中，这两个向量构造的边界实际上是同一条。

因此，问题就转化为了这些边界中，总共有多少个向量是极角不同的。

以$y$轴正半轴为基准，那么不难发现，正$n$变形的边界的极角分别是$0,\dfrac{1}{n}\cdot 2\pi,\dfrac{2}{n}\cdot 2\pi,\dots,\dfrac{n-1}{n}\cdot 2\pi$。

那么问题进一步转化成：分母在范围$1864\sim 1909$的**真分数**中，一共有多少个不同值的分数（包括$0$）？



## 代码


```py
from fractions import Fraction

L, R = 1864, 1909
ans = len(set(Fraction(i, j) for j in range(L, R + 1) for i in range(j)))
print(ans)

```