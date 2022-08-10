---
title: Project Euler 607
date: 2022-04-22 11:10:50
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 607

## 题目

### Marsh Crossing

Frodo and Sam need to travel $100$ leagues due East from point $A$ to point $B$. On normal terrain, they can cover $10$ leagues per day, and so the journey would take $10$ days. However, their path is crossed by a long marsh which runs exactly South-West to North-East, and walking through the marsh will slow them down. The marsh is $50$ leagues wide at all points, and the mid-point of $AB$ is located in the middle of the marsh. A map of the region is shown in the diagram below:

![](../images/p607_marsh.png)

The marsh consists of $5$ distinct regions, each $10$ leagues across, as shown by the shading in the map. The strip closest to point $A$ is relatively light marsh, and can be crossed at a speed of $9$ leagues per day. However, each strip becomes progressively harder to navigate, the speeds going down to $8, 7, 6$ and finally $5$ leagues per day for the final region of marsh, before it ends and the terrain becomes easier again, with the speed going back to $10$ leagues per day.

If Frodo and Sam were to head directly East for point $B$, they would travel exactly $100$ leagues, and the journey would take approximately $13.4738$ days. However, this time can be shortened if they deviate from the direct path.

Find the shortest possible time required to travel from point $A$ to $B$, and give your answer in days, rounded to $10$ decimal places.

## 折射定律/斯涅尔定律(Snell's Law)

### 费马原理

[费马原理](https://en.wikipedia.org/wiki/Fermat%27s_principle)，法国科学家皮埃尔·德·费马在1662年提出：**光传播的路径是光程取极值的路径**。这个极值可能是最大值、最小值，甚至是函数的拐点。最初提出时，又名“**最短时间原理**”：光线传播的路径是需时最少的路径。由费马原理可以导出斯涅尔定律。

### 折射定律

[斯涅尔定律](https://en.wikipedia.org/wiki/Snell%27s_law)，假设光在介质1传播的速率为$v_1$，在介质2的传播速率为$v_2$。那么介质1的折射率为$n_1=\frac{c}{v_1}$，介质2的折射率为$n_2=\frac{c}{v_2}$，其中$c$为光速。

光线从介质1在某一点$O$传播进入介质2，$\theta_1$为入射角，$\theta_2$为折射角。

那么有折射定律：

$$n_1\sin \theta_1=n_2\sin\theta_2$$

## 解决方案

由于此时需要从$A$到$B$的时间最短，并且各沼泽段的行走速度不一样。可以将各沼泽段分别视为“介质”，对应的行走速度视为光的传播速率，然后根据斯涅尔定律，一束“光”从A射向B，计算其最短时间即可。

本代码使用二分法确定“入射角”，此时判断的是“光”最终射向点B的左侧还是右侧，并且在过程中计算“光程”。

## 代码

```Python
from math import sin, pi

s = d = 100 / 2 ** 0.5
v = [10, 9, 8, 7, 6, 5, 10]
dis = [(d - 50) / 2, 10, 10, 10, 10, 10, (d - 50) / 2]
l, r = 0, pi / 2
ans = 0
for _ in range(100):
    mid = 0.5 * (l + r)
    sinv = [sin(mid)]
    for i in range(1, len(v)):
        sinv.append(sinv[0] / v[0] * v[i])
    tm = 0
    len_x = 0
    for i in range(len(v)):
        sin_val = sinv[i]
        cos_val = (1 - sin_val ** 2) ** 0.5
        tan_val = sin_val / cos_val
        d = dis[i] / cos_val
        tm += d / v[i]
        len_x += dis[i] * tan_val
    if len_x < s:
        l = mid
    else:
        r = mid
    ans = tm
print("{:.10f}".format(ans))
```
