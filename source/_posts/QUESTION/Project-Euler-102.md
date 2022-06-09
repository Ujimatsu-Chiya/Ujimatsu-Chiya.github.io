---
title: Project Euler 102
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:23:21
---

<escape><!-- more --></escape>

# Project Euler 102

## 题目

### Triangle containment

Three distinct points are plotted at random on a Cartesian plane, for which $-1000 \leq x,y\leq  1000$, such that a triangle is formed.

Consider the following two triangles:

$$A(-340,495), B(-153,-910), C(835,-947)$$
$$X(-175,41), Y(-421,-714), Z(574,-645)$$

It can be verified that triangle $ABC$ contains the origin, whereas triangle $XYZ$ does not.

Using [triangles.txt](../resources/p102_triangles.txt) (right click and 'Save Link/Target As\dots'), a 27K text file containing the co-ordinates of one thousand "random" triangles, find the number of triangles for which the interior contains the origin.

NOTE: The first two examples in the file represent the triangles in the example given above.

## 解决方案

设向量$\overrightarrow{a}=(x_1,y_1),\overrightarrow{b}=(x_2,y_2)$。那么向量的叉积为

$$\overrightarrow{a}\times \overrightarrow{b}=x_1y_2-x_2y_1=|\overrightarrow{a}||\overrightarrow{b}|\sin\theta$$

其中$\theta$为$\overrightarrow{a}$逆时针旋转到$\overrightarrow{b}$的角度。

如果向量$\overrightarrow{b}$的方向为向量$\overrightarrow{a}$逆时针旋转$180°$内，那么$\overrightarrow{a}\times\overrightarrow{b}>0$。

因此，对于$\triangle ABC$任意内一点$P$，如果$\overrightarrow{PA}\times \overrightarrow{PB},\overrightarrow{PB}\times \overrightarrow{PC},\overrightarrow{PC}\times \overrightarrow{PA}$有一个值为$0$，那么$P$在$\triangle ABC$边上。如果三个值的正负性都相同，那么$P$在$\triangle ABC$内部。否则P在$\triangle ABC$外部。

## 代码

```py
def cross(va: tuple, vb: tuple):
    return va[0] * vb[1] - va[1] * vb[0]


def ok(vec_list: list):
    u, v, w = cross(vec_list[0], vec_list[1]), cross(vec_list[1], vec_list[2]), cross(vec_list[2], vec_list[0])
    if u > 0 and v > 0 and w > 0 or u < 0 and v < 0 and w < 0:
        return True
    return False


ls = open('p102_triangles.txt', 'r').readlines()
ans = 0
for s in ls:
    t = [int(x) for x in s.split(',')]
    if ok([(t[0], t[1]), (t[2], t[3]), (t[4], t[5])]):
        ans += 1
print(ans)

```
