---
title: Project Euler 43
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 43
## 题目
### Sub-string divisibility
The number, $1406357289$, is a $0$ to $9$ pandigital number because it is made up of each of the digits $0$ to $9$ in some order, but it also has a rather interesting sub-string divisibility property.

Let $d_1$ be the 1st digit, $d_2$ be the 2nd digit, and so on. In this way, we note the following:

$d_2d_3d_4=406$ is divisible by $2$
$d_3d_4d_5=063$ is divisible by $3$
$d_4d_5d_6=635$ is divisible by $5$
$d_5d_6d_7=357$ is divisible by $7$
$d_6d_7d_8=572$ is divisible by $11$
$d_7d_8d_9=728$ is divisible by $13$
$d_8d_9d_{10}=289$ is divisible by $17$

Find the sum of all $0$ to $9$ pandigital numbers with this property.

## 解决方案

可以直接用itertools库中的permutations产生所有置换，然后一个个直接进行判断。

比较一种优化的方法是自己手写dfs生成全排列，但是在恰当的地方及时剪枝，这将比上面的方法快不少。

## 代码
```py
t = "0123456789"
ans = 0
for x in permutations(t):
    s = "".join(x)
    ok = 1
    if int(s[1:4]) % 2 != 0 or int(s[2:5]) % 3 != 0 or int(s[3:6]) % 5 != 0 or int(s[4:7]) % 7 != 0 or \
            int(s[5:8]) % 11 != 0 or int(s[6:9]) % 13 != 0 or int(s[7:10]) % 17 != 0:
        ok = 0
    if ok:
        ans += int(s)
print(ans)
```
```py
N = 10
vis = [0 for i in range(N)]
val = [0 for i in range(N)]
m = [2, 3, 5, 7, 11, 13, 17]
ans = 0


def dfs(f: int):
    global ans
    if f == 10:
        ans += int("".join(str(x) for x in val))
        return

    for i in range(10):
        if vis[i]:
            continue
        if f == 0 and i == 0:
            continue
        if f >= 3:
            if (val[f - 2] * 100 + val[f - 1] * 10 + i) % m[f - 3] != 0:
                continue
        val[f] = i
        vis[i] = True
        dfs(f + 1)
        vis[i] = False


dfs(0)
print(ans)
```