---
title: Project Euler 244
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-04 18:02:37
---

<escape><!-- more --></escape>

# Project Euler 244

## 题目

### Sliders

You probably know the game *Fifteen Puzzle*. Here, instead of numbered tiles, we have seven red tiles and eight blue tiles.

A move is denoted by the uppercase initial of the direction (Left, Right, Up, Down) in which the tile is slid, e.g. starting from configuration (**S**), by the sequence **LULUR** we reach the configuration (**E**):

(**S**)![](../images/p244_start.gif),(**E**)![](../images/p244_example.gif)

For each path, its checksum is calculated by (pseudocode):

$\begin{aligned}
\text{checksum} &= 0\\
\text{checksum} &= (\text{checksum} \times 243 + m_1) \mod 100000007\\
\text{checksum} &= (\text{checksum} \times 243 + m_2) \mod 100000007\\
&\dots&\\
\text{checksum} &= (\text{checksum} \times 243 + m_n) \mod 100000007
\end{aligned}$

where $m_k$ is the ASCII value of the $k^{\text{th}}$ letter in the move sequence and the ASCII values for the moves are:

|||
|-|-|
|**L**|$76$|
|**R**|$82$|
|**U**|$85$|
|**D**|$68$|

For the sequence **LULUR** given above, the checksum would be $19761398$.
Now, starting from configuration (**S**), find all shortest ways to reach configuration (**T**).

(**S**)![](../images/p244_start.gif),(**T**)![](../images/p244_target.gif)

What is the sum of all checksums for the paths having the minimal length?

## 解决方案

考虑使用广度优先搜素进行，从节点**S**到节点**T**处理出所有路径。

不过，在实际的实现过程中发现，如果从**S**到某个节点**U**的最短路径$\text{checksum}$之和，全部乘$243$再添加一个方向的ASCII码后就可以成为下一个未遍历节点的$\text{checksum}$之和的一部分。因此实际上不需要求出所有最短路径并枚举，只需要维护**S**到当前的节点的$\text{checksum}$之和即可。

为了节省存储空间，将棋盘编码成了一个$16$位三进制数，以作为两个字典的键。

## 代码

```py
from queue import Queue

st = [[0, 1, 2, 2], [1, 1, 2, 2], [1, 1, 2, 2], [1, 1, 2, 2]]
ed = [[0, 2, 1, 2], [2, 1, 2, 1], [1, 2, 1, 2], [2, 1, 2, 1]]
dx, dy, code = [0, 0, -1, 1], [-1, 1, 0, 0], [82, 76, 68, 85]
mod = 100000007


def encode(a: list):
    ans = 0
    for i in range(4):
        for j in range(4):
            ans = ans * 3 + a[i][j]
    return ans


dis = {encode(st): 0}
val = {encode(st): 0}
q = Queue()
q.put(st)
while not q.empty():
    u = q.get()
    pre = encode(u)
    for i in range(16):
        # 以一重循环代替二重循环，i>>2为行号，i&3为列号
        if u[i >> 2][i & 3] == 0:
            x, y = i >> 2, i & 3
            break
    for k in range(4):
        nx, ny = x + dx[k], y + dy[k]
        if nx < 0 or ny < 0 or nx >= 4 or ny >= 4:
            continue
        v = [a.copy() for a in u]
        v[nx][ny], v[x][y] = v[x][y], v[nx][ny]
        now = encode(v)
        if now not in dis.keys():
            dis[now] = dis[pre] + 1
            val[now] = 0
            q.put(v)
        if dis[now] == dis[pre] + 1:
            val[now] = (val[now] + val[pre] * 243 + code[k]) % mod
ans = val[encode(ed)]
print(ans)

```
