---
title: Project Euler 220
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-01 17:37:28
---

<escape><!-- more --></escape>

# Project Euler 220

## 题目

### Heighway Dragon

Let $\mathbf{D}_0$ be the two-letter string “Fa”. For $n\ge1$, derive $\mathbf{D}_n$ from $\mathbf{D}_{n-1}$ by the string-rewriting rules:

“a” → “aRbFR”<br>“b” → “LFaLb”

Thus, $\mathbf{D}_0$ = “Fa”, $\mathbf{D}_1$ = “FaRbFR”, $\mathbf{D}_2$ = “FaRbFRRLFaLbFR”, and so on.

These strings can be interpreted as instructions to a computer graphics program, with “F” meaning “draw forward one unit”, “L” meaning “turn left $90$ degrees”, “R” meaning “turn right $90$ degrees”, and “a” and “b” being ignored. The initial position of the computer cursor is $(0,0)$, pointing up towards $(0,1)$.

Then $\mathbf{D}_n$ is an exotic drawing known as the *Heighway Dragon* of order $n$.  For example, $\mathbf{D}_{10}$ is shown below; counting each “F” as one step, the highlighted spot at $(18,16)$ is the position reached after $500$ steps.

![](../images/p220.gif)

What is the position of the cursor after $10^{12}$ steps in $D_{50}$ ?

Give your answer in the form $x,y$ with no spaces.

## 解决方案

令$N=10^{12}$。并假设机器人第$i$步走到的点为$(x_i,y_i)$。

令$a_0=\emptyset,b_0=\emptyset$，那么可以写出

$\begin{aligned}
a_n&\rightarrow a_{n-1}Rb_{n-1}FR\\
b_n&\rightarrow LFa_{n-1}Lb_{n-1}\\
D_n&\rightarrow Fa_n
\end{aligned}$

令$D_n'\rightarrow b_{n-1}F$，那么可以将$a_n,b_n$从这些规则中消去：

$\begin{aligned}
D_n&\rightarrow Fa_n\rightarrow Fa_{n-1}Rb_{n-1}FR\rightarrow D_{n-1}RD_{n-1}'R\\
D_n'&\rightarrow b_nF\rightarrow LFa_{n-1}Lb_{n-1}F\rightarrow LD_{n-1}LD_{n-1}'\\
\end{aligned}$

最终这些规则可以写成：

$\begin{aligned}
D_0&\rightarrow F\\
D_0'&\rightarrow F\\
D_n&\rightarrow D_{n-1}RD_{n-1}'R\\
D_n'&\rightarrow LD_{n-1}LD_{n-1}'\\
\end{aligned}$

可以发现，$D_{n-1}$是$D_n$的前缀，那么实际上可以将$D$可以看成是一个无限字符串。并且，如果走完$D_n$或者是$D_n'$中的所有步骤，那么就相当于已经行走了$2^n$步。

考虑动态规划的思想，从原点开始，如果运行完$D_n$或者是$D_n'$中所有的指令后，当前机器人所处的位置和旋转的角度，用一个三元组$(x,y,d)$来表示。那么，就按照给定的规则，逐步递推到运行第$N$个$F$的地方。

另外，在该[页面](https://en.wikipedia.org/wiki/Dragon_curve)中查询到了这种龙形曲线的一些信息：在第$m$次迭代前，龙形曲线的最后一段端点在$(a_{m-1},b_{m-1})$处。那么，将整个龙形曲线**逆时针**旋转$90°$，原点$(0,0)$的位置将被旋转到$(a_m,b_m)$，旋转前和旋转后的曲线合并在一起就是第$n$轮的迭代结果。另外，$(a_0,b_0)=(0,1)$。并且，可以发现$(x_{2^m},y_{2^m})=(a_m.b_m)$

这启发我们给出了寻找坐标点另一个更简单的算法：如果需要求第$n$次行走的结果，那么需要找到最小的整数$t$使得$2^t\ge n$，那么第$n$步的结果就相当于是将第$2^t-n$步的点$(x_{2^t-n},y_{2^t-n})$绕$(x_{2^{t-1}},y_{2^{t-1}})$点逆时针旋转$90°$得到。这相当于将问题转化成了两个子问题：找出点$(x_{2^{t-1}},y_{2^{t-1}})$点$(x_{2^t-n},y_{2^t-n})$的坐标。逐步递归即可得到最终答案。

## 代码

```py
N = 10 ** 12


def f(now: tuple, *dir_list):
    x, y, d = now
    for dif in dir_list:
        if d == 0:
            x, y = x + dif[0], y + dif[1]
        elif d == 1:
            x, y = x - dif[1], y + dif[0]
        elif d == 2:
            x, y = x - dif[0], y - dif[1]
        else:
            x, y = x + dif[1], y - dif[0]
        d = (d + dif[2]) % 4
    return x, y, d


l = len(bin(N)) - 2
F, L, R = (0, 1, 0), (0, 0, 1), (0, 0, -1)
Da = [F]
Db = [F]
for i in range(1, l + 1):
    Da.append(f(Da[i - 1], R, Db[i - 1], R))
    Db.append(f(L, Da[i - 1], L, Db[i - 1]))
now = (0, 0, 0)
flag = 0
for i in range(l - 1, -1, -1):
    if flag == 0:
        if N >> i & 1:
            now = f(now, Da[i], R)
            flag = 1
        else:
            flag = 0
    else:
        now = f(now, L)
        if N >> i & 1:
            now = f(now, Da[i], L)
            flag = 1
        else:
            flag = 0
ans = ",".join(str(x) for x in now[:2])
print(ans)

```

```py
N = 10 ** 12
mp = {0: (0, 0), 1: (0, 1)}


def cal(c, p):
    cx, cy = c
    px, py = p
    return cx - py + cy, cy + px - cx


def find(n):
    if n in mp.keys():
        return mp[n]
    pw = 1
    while pw < n:
        pw *= 2
    mp[n] = cal(find(pw // 2), find(pw - n))
    return mp[n]


ans = ",".join(str(x) for x in find(N))
print(ans)

```
