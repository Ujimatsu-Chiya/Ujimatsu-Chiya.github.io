---
title: Project Euler 151
tags:
  - Project Euler
  - 动态规划
  - 概率
mathjax: true
date: 2022-05-08 11:56:18
---

<escape><!-- more --></escape>

# Project Euler 151

## 题目

### Paper sheets of standard sizes: an expected-value problem

A printing shop runs $16$ batches (jobs) every week and each batch requires a sheet of special colour-proofing paper of size A5.

Every Monday morning, the foreman opens a new envelope, containing a large sheet of the special paper with size A1.

He proceeds to cut it in half, thus getting two sheets of size A2. Then he cuts one of them in half to get two sheets of size A3 and so on until he obtains the A5-size sheet needed for the first batch of the week.

All the unused sheets are placed back in the envelope.

![](../images/p151.png)

At the beginning of each subsequent batch, he takes from the envelope one sheet of paper at random. If it is of size A5, he uses it. If it is larger, he repeats the ‘cut-in-half’ procedure until he has what he needs and any remaining sheets are always placed back in the envelope.

Excluding the first and last batch of the week, find the expected number of times (during each week) that the foreman finds a single sheet of paper in the envelope.

Give your answer rounded to six decimal places using the format x.xxxxxx.

## 解决方案

本题是一道比较明显的期望动态规划题，状态比较明显。

每个状态用一个五元组$(i_1,i_2,i_3,i_4,i_5)$为袋子里目前剩下纸张的情况，其中$i_j$就代表着剩下$i_j$张大小为Aj的纸。

令$f(i_1,i_2,i_3,i_4,i_5)$为在这种剩余纸张情况下，未来会遇见一张纸的期望次数。

题目中要求等概率地随机抽取一张纸：

1. 如果是A5直接用掉，相当于从$(i_1,i_2,i_3,i_4,i_5-1)$中转移过来。
2. 否则，他会一直裁纸，直到见到一张A5，并且使用它。那么这种情况下如果是遇到Aj大小的纸，那么就是从$(i_1,i_2,\dots,i_{j-1},\mathbf{i_j-1,i_{j+1}+1},\dots,i_5+1)$转移过来。注意加粗的地方，使用的纸被消耗了，比它更小的纸都增加了一张。

因此，状态转移方程如下：

$$
f(i_1,i_2,i_3,i_4,i_5)=
\left \{\begin{aligned}
  &0  & & \mathrm{if\quad} \sum_{k=1}^5=0 \\
  &\sum_{j=1,i_j>0}^5f(\dots,i_{j-1},i_{j}-1,i_{j+1}+1,\dots)\dfrac{i_k}{\sum_{k=1}^5i_k}+[\sum_{k=1}^5i_k=1] & & \mathrm{else}
\end{aligned}\right.
$$

其中，$[]$表示示性函数，表示$[]$里面的值是否为真，如果为真，那么值为$0$，否则值为$1$.

整个递归的边界是纸被用完了，故值为$0$.

最终答案为$f(1,0,0,0,0)-2$，因为题目要求减去第一次和最后一次见到一张纸的情况。

## 代码

```py
mp = {(0, 0, 0, 0, 0): 0}


def dfs(tp: tuple):
    if tp in mp.keys():
        return mp[tp]
    s = sum(tp)
    val = (s == 1)
    for i in range(5):
        if tp[i] == 0:
            continue
        ls = list(tp)
        ls[i] -= 1
        for j in range(i + 1, 5):
            ls[j] += 1
        val += dfs(tuple(ls)) * tp[i] / s
    mp[tp] = val
    return val


ans = dfs((1, 0, 0, 0, 0)) - 2
print("{:.6f}".format(ans))

```
