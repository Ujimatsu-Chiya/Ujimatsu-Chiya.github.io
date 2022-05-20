---
title: Project Euler 161
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 161
## 题目
### Triominoes
A triomino is a shape consisting of three squares joined via the edges. There are two basic forms:

![](../images/p161_trio1.gif)

If all possible orientations are taken into account there are six:

![](../images/p161_trio3.gif)


Any $n$ by $m$ grid for which $n\times m$ is divisible by $3$ can be tiled with triominoes.

If we consider tilings that can be obtained by reflection or rotation from another tiling as different there are $41$ ways a $2$ by $9$ grid can be  tiled with triominoes:

![](../images/p161_k9.gif)

In how many ways can a $9$ by $12$ grid be tiled in this way by triominoes?


## 解决方案


## 代码


```py
N, M = 9, 12
triomino_ls = [
    [(0, 0), (1, 0), (0, 1)],
    [(0, 0), (1, 0), (1, 1)],
    [(0, 0), (0, 1), (1, 1)],
    [(0, 0), (1, 0), (1, -1)],
    [(0, 0), (0, 1), (0, 2)],
    [(0, 0), (1, 0), (2, 0)],
]
if M > N:
    N, M = M, N


def get_empty(grid: tuple):
    for i in range(len(grid)):
        if grid[i] != (1 << M) - 1:
            for j in range(M):
                if (grid[i] >> j & 1) == 0:
                    return i, j
    return None


def place_triomino(grid: tuple, x: int, y: int, id: int):
    tp = list(grid)
    for dx, dy in triomino_ls[id]:
        nx, ny = x + dx, y + dy
        if nx < 0 or ny < 0 or nx >= len(grid) or ny >= M or tp[nx] >> ny & 1:
            return None
        tp[nx] |= 1 << ny
    while len(tp) > 0 and tp[0] == (1 << M) - 1:
        del tp[0]
    return tuple(tp)


cnt = M * N // 3
st = tuple(0 for i in range(N))
f = [{} for i in range(cnt + 1)]
f[0][st] = 1
for i in range(cnt):
    for grid, val in f[i].items():
        x, y = get_empty(grid)
        for k in range(6):
            next = place_triomino(grid, x, y, k)
            if next is None:
                continue
            if next not in f[i + 1].keys():
                f[i + 1][next] = 0
            f[i + 1][next] += val
ans = list(f[cnt].values())[0]
print(ans)

```