---
title: Project Euler 166
tags:
  - Project Euler
  - meet-in-the-middle
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 166
## 题目
### Criss Cross

A $4\times 4$ grid is filled with digits $d$, $0 \le d \le 9$.

It can be seen that in the grid

$$\begin{matrix}
6 & 3 & 3 & 0 \\
5 & 0 & 4 & 3 \\
0 & 7 & 1 & 4 \\
1 & 2 & 4 & 5
\end{matrix}$$
the sum of each row and each column has the value $12$. Moreover the sum of each diagonal is also $12$.

In how many ways can you fill a $4\times 4$ grid with the digits $d$, $0 \le d \le 9$ so that each row, each column, and both diagonals have the same sum?



## 解决方案

本题基于meet-in-the-middle的思想完成。

首先枚举幻方一行中所有的可能性填法，按照行的和分别存储，共$10000$种可能的填法。

接下来，枚举前两行的填法。

第二行元素的和$s$必须和第一行相同（这就是按和分类存储的原因）。这时就枚举了整个幻方的一半数字。用一个六元组$(a,b,c,d,e,f)$分别统计这一半的填法分别有多少，其中，$a,b,c,d$分别表示幻方$4$列上的两个数的和，$e,f$则表示主副对角线上两个数的和。

不失一般性，幻方的下两行和上两行的枚举方式是完全一样的。下面两行如果存在一种填法$(a,b,c,d,e,f)$，那么上面两行的填法一定是$(s-a,s-b,s-c,s-d,s-e,s-f)$。

直接统计这种做法个数之和。

## 代码


```py
mp = {}
ans = 0
for i in range(10):
    for j in range(10):
        for k in range(10):
            for l in range(10):
                w = i + j + k + l
                if w not in mp.keys():
                    mp[w] = []
                mp[w].append((i, j, k, l))
for s, vec in mp.items():
    mq = {}
    for u in vec:
        for v in vec:
            t = (u[0] + v[0], u[1] + v[1], u[2] + v[2], u[3] + v[3], u[0] + v[1], u[3] + v[2])
            if t not in mq:
                mq[t] = 0
            mq[t] += 1
    for u in vec:
        for v in vec:
            t = (s - u[0] - v[0], s - u[1] - v[1], s - u[2] - v[2], s - u[3] - v[3], s - u[2] - v[3], s - u[1] - v[0])
            if t in mq:
                ans += mq[t]
print(ans)

```