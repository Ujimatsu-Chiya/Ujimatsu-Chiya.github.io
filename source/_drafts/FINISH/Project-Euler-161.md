---
title: Project Euler 161
tags:
  - Project Euler
  - 动态规划
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

一个明显的优化：如果列的长度比行大，那么可以行列互换。为了加速，明显应该用位运算来表示列的状态（因为它的长度短）。

使用动态规划的思想进行计数。为了使得计数不重合，那么使用以下方法：每次选定填充的格子，必定是行下标最下的格子（如果有多个，那么就选列下标最小的）。在这个选定的格子中，依次尝试填入$6$个种类的方块。

由于每次填入的方块最多$3$行，因此本代码记录状态时，每次都要表示$3$行的状态。

如果发现第一行被填完了，那么就可以忽略掉这一行，直接从下一行开始填。

本题还使用记忆化搜索，避免再度搜索已经检查过的状态。

下面的py代码是解答时写的，C++代码是解答后看了一些优化方案然后再写的。

## 代码
```C++
# include <bits/stdc++.h>
# define Y second
typedef long long ll;
using namespace std;

const int H = 9, W = 12;
const int N = max(H, W), M = min(H, W);
const int msk = (1 << M) - 1;

int low_zero[1<<M];
unordered_map<ll, ll> mp[N + 2];


ll dfs(int f, int r1, int r2, int r3) {
    if (f == 0)
        return 1;
    if (r1 == msk)
        return dfs(f - 1, r2, r3, 0);
    ll h = (r1 << M | r2) << M | r3;
    auto it = mp[f].find(h);
    if (it != mp[f].end())
        return it->Y;
    int pos = low_zero[r1];
    ll ans = 0;
    // 1
    if (f >= 2 && pos < M - 1 && !(r1 >> pos & 3) && !(r2 >> pos & 1))
        ans += dfs(f, r1|3<<pos, r2|1<<pos, r3);

    // 2
    if (f >= 2 && pos < M - 1 && !(r1 >> pos & 3) && !(r2 >> pos & 2))
        ans += dfs(f, r1|3<<pos, r2|2<<pos, r3);

    // 3
    if (f >= 2 && pos < M - 1 && !(r1 >> pos & 1) && !(r2 >> pos & 3))
        ans += dfs(f, r1|1<<pos, r2|3<<pos, r3);

    // 4
    if (f >= 2 && pos > 0 && pos < M && !(r1 >> pos & 1) && !(r2 >> (pos - 1) & 3))
        ans += dfs(f, r1|1<<pos, r2|3<<(pos-1), r3);

    // 5
    if (f >= 3 && !((r1 | r2 | r3) >> pos & 1))
        ans += dfs(f, r1 | 1 << pos, r2 | 1 << pos, r3 | 1 << pos);

    // 6
    if (f >= 1 && pos < M - 2 && !(r1 >> pos & 7))
        ans += dfs(f, r1 | 7 << pos, r2, r3);

    return mp[f][h] = ans;
}

int main() {
    for (int s = 0; s < (1 << M); s++)
        for (low_zero[s] = 0; low_zero[s] < M && (s >> low_zero[s] & 1); low_zero[s]++);
    ll ans = dfs(N, 0, 0, 0);
    printf("%lld\n", ans);
    return 0;
}
```

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