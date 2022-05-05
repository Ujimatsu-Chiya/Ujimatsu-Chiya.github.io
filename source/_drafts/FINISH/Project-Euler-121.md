---
title: Project Euler 121
tags:
  - Project Euler
  - 概率
  - 动态规划
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 121
## 题目
### Disc game prize fund


A bag contains one red disc and one blue disc. In a game of chance a player takes a disc at random and its colour is noted. After each turn the disc is returned to the bag, an extra red disc is added, and another disc is taken at random.

The player pays $£1$ to play and wins if they have taken more blue discs than red discs at the end of the game.

If the game is played for four turns, the probability of a player winning is exactly $\dfrac{11}{120}$, and so the maximum prize fund the banker should allocate for winning in this game would be $£10$ before they would expect to incur a loss. Note that any payout will be a whole number of pounds and also includes the original $£1$ paid to play the game, so in the example given the player actually wins $£9$.

Find the maximum prize fund that should be allocated to a single game in which fifteen turns are played.


## 解决方案

第一个问题：赢的概率有多大。

本题状态转移比较明显，可以使用基于概率的动态规划解决问题。

令游戏轮数$n=15$，那么设状态$f(i,j)(0\le j\le i\le n)$为：完成了$i$轮的游戏后，得到$j$个蓝色碟子的概率。可以列出以下状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=0\&j=0 \\
  &f(i-1,j) \cdot \dfrac{i}{i+1}  & & \mathrm{if\quad} j=0\\
  &f(i-1,j-1) \cdot \dfrac{1}{i+1}  & & \mathrm{if\quad} j=i\\
  &f(i-1,j) \cdot \dfrac{i}{i+1} + f(i-1,j-1) \cdot \dfrac{1}{i+1} & & \mathrm{else}
\end{aligned}\right.
$$

对于最后一行，要么从上一轮的状态$f(i-1,j)$以$\dfrac{i}{i+1}$抽到一个红色碟子转移而来，或者是从$f(i-1,j-1)$以$\dfrac{1}{i+1}$的概率抽到一个蓝色碟子。

因此，胜利的情况概率为$\sum_{i=\lfloor\frac{n}{2}+1\rfloor}^n f(n,i)$.

第二个问题：为防止游戏亏损，至多设立的钱数是多少。

假设$X$为玩家进行一次游戏所获得的钱数，那么$X$满足以下两点分布：

|$X$|$P(X)$|
|-|-|
|$\sum_{i=\lfloor\frac{n}{2}+1\rfloor}^n f(n,i)$|$x-1$|
|$1-\sum_{i=\lfloor\frac{n}{2}+1\rfloor}^n f(n,i)$|$-1$|

为了防止游戏亏损，那么$X$的数学期望$E[X]$必须满足$E[X]<0$。

由于$x$必须是整数，因此可以解得最高奖金数$x=\lfloor\dfrac{1}{\sum_{i=\lfloor\frac{n}{2}+1\rfloor}^n f(n,i)}\rfloor$

## 代码


```py
N = 15
f = [[1]]

for i in range(1, N + 1):
    ls = [0 for j in range(i + 1)]
    f.append(ls)
    for j in range(i + 1):
        if j > 0:
            f[i][j] += f[i - 1][j - 1] * 1 / (i + 1)
        if j < i:
            f[i][j] += f[i - 1][j] * i / (i + 1)
ans = 0
for j in range(N + 1):
    if j > N - j:
        ans += f[N][j]
print(int(1 / ans))

```