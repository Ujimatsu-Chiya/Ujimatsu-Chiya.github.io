---
title: Project Euler 247
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 247

## 题目

### Squares under a hyperbola

Consider the region constrained by $1 \le x$ and $0 \le y \le \dfrac{1}{x}$.

Let $S_1$ be the largest square that can fit under the curve.

Let $S_2$ be the largest square that fits in the remaining area, and so on.

Let the *index* of $S_n$ be the pair (left, below) indicating the number of squares to the left of $S_n$ and the number of squares below $S_n$.

![](../images/p247_hypersquares.gif)

The diagram shows some such squares labelled by number.

$S_2$ has one square to its left and none below, so the index of $S_2$ is $(1,0)$.

It can be seen that the index of $S_{32}$ is $(1,1)$ as is the index of $S_{50}$.

$50$ is the largest $n$ for which the index of $S_n$ is $(1,1)$.

What is the largest $n$ for which the index of $S_n$ is $(3,3)$?

## 解决方案
假设当前正方形的左下角顶点为$(x_0,y_0)$，那么通过以下步骤可以计算这个正方形的最大边长：
1. 联立两个方程：$y=\dfrac{1}{x},y-y_0=x-x_0$，最终解得出右上角的定点为$(x,y)$
2. 这个正方形的边长为$x-x_0$。

为了进行加速，代码实现没有使用[优先队列](https://en.wikipedia.org/wiki/Priority_queue)，而是使用了两次深度优先搜索：

- 第一次用于找到坐标为$(3,3)$的最小正方形，假设边长$l$。
- 第二次用于找到比$l$大的所有正方形边长。

两次搜索完成后，找到的个数加$1$就是答案。

由于第二次深度优先搜索递归深度太大，故使用非递归进行模拟。
## 代码
```py
N = 3
M = 3
min_size = 1
ans = 1


def cal(x, y):
    b = y - x
    return (-b + (b ** 2 + 4) ** 0.5) / 2 - x


def dfs(x, y, fx, fy):
    if fx > N or fy > M:
        return
    size = cal(x, y)
    global min_size
    if fx == N and fy == M and size < min_size:
        min_size = size
    dfs(x + size, y, fx + 1, fy)
    dfs(x, y + size, fx, fy + 1)


dfs(1, 0, 0, 0)
st = [(1, 0)]
while len(st) > 0:
    x, y = st.pop()
    size = cal(x, y)
    if size > min_size:
        ans += 1
        st.append((x + size, y))
        st.append((x, y + size))
print(ans)

```