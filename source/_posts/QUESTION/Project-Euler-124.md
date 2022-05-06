---
title: Project Euler 124
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:24:49
---

<escape><!-- more --></escape>
   

# Project Euler 124
## 题目
### Ordered radicals
The radical of $n$, $\mathrm{rad}(n)$, is the product of the distinct prime factors of $n$. For example, $504 = 2^3 × 3^2 × 7$, so $\mathrm{rad}(504) = 2 × 3 × 7 = 42$.

If we calculate $\mathrm{rad}(n)$ for $1 \le n \le 10$, then sort them on rad(n), and sorting on n if the radical values are equal, we get:

||**Unsorted**|||**Sorted**||
|-|-|-|-|-|-|
|$\mathbf{n}$|$\mathbf{rad}(n)$||$\mathbf{n}$|$\mathbf{rad}(n)$|$\mathbf{k}$|
|$1$|$1$||$1$|$1$|$1$|
|$2$|$2$||$2$|$2$|$2$|
|$3$|$3$||$4$|$2$|$3$|
|$4$|$2$||$8$|$2$|$4$|
|$5$|$5$||$3$|$3$|$5$|
|$6$|$6$||$9$|$3$|$6$|
|$7$|$7$||$5$|$5$|$7$|
|$8$|$2$||$6$|$6$|$8$|
|$9$|$3$||$7$|$7$|$9$|
|$10$|$10$||$10$|$10$|$10$|


Let $E(k)$ be the $k\mathrm{th}$ element in the sorted n column; for example, $E(4) = 8$ and $E(6) = 9$.

If $\mathrm{rad}(n)$ is sorted for $1 \le n \le 100000$, find $E(10000)$.


## 解决方案

使用埃氏筛，可以标记出所有质数，并对质数的倍数进行标记。而在标记的过程中，则将对应的$\mathrm{rad}$函数值数组乘上这个质数。整个埃氏筛结束后，$\mathrm{rad}$数组里面的所有函数值就计算可以完成。

同样，线性筛也可以完成这个工作。

排序后即可得到答案。

## 代码

```py
N = 10 ** 5
Q = 10 ** 4
rad = [1 for _ in range(N + 1)]
rank = [i for i in range(1, N + 1)]
for i in range(2, N + 1):
    if rad[i] == 1:
        for j in range(i, N + 1, i):
            rad[j] *= i
rank.sort(key=lambda x: (rad[x], x))
ans = rank[Q - 1]
print(ans)

```
