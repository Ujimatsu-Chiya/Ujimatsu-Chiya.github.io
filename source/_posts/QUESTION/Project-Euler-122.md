---
title: Project Euler 122
tags:
  - Project Euler
  - OEIS
mathjax: true
date: 2022-05-06 22:24:41
---

<escape><!-- more --></escape>
    

# Project Euler 122
## 题目
### Efficient exponentiation
The most naive way of computing n^15 requires fourteen multiplications:

$n \times n \times \dots \times n = n^{15}$

But using a “binary” method you can compute it in six multiplications:

$\begin{aligned}
n \times n &= n^2\\
n^2 \times n^2 &= n^4\\
n^4 \times n^4 &= n^8\\
n^8 \times n^4 &= n^{12}\\
n^{12} \times n^2 &= n^{14}\\
n^{14} \times n &= n^{15}
\end{aligned}$

However it is yet possible to compute it in only five multiplications:

$\begin{aligned}
n \times n &= n^2\\
n^2 \times n &= n^3\\
n^3 \times n^3 &= n^6\\
n^6 \times n^6 &= n^{12}\\
n^{12} \times n^3 &= n^{15}
\end{aligned}$

We shall define $m(k)$ to be the minimum number of multiplications to compute $n^k$; for example $m(15) = 5$.

For $1 \le k \le 200$, find $\sum m(k)$.


## 解决方案

本题基于深度优先搜索的剪枝。

为了尽快使结果收敛，可以为每个数的答案先拟定一个上限，而这个上限就是但使用题目所提供的“二进制”的算法（也就是快速幂）。

求出前几项后，在OEIS找到了该数列[A003313](https://oeis.org/A003313)。在FORMULA一栏中，找到了以下信息:

```
For all n >= 2, a(n) <= (4/3)*floor(log_2 n) + 2. - Jonathan Vos Post, Oct 08 2008
From Achim Flammenkamp, Oct 26 2016: (Start)
a(n) <= 9/log_2(71) log_2(n), for all n.
It is conjectured by D. E. Knuth, K. Stolarsky et al. that for all n: floor(log_2(n)) + ceiling(log_2(v(n))) <= a(n). (End)
```

这说明，值的上限还可以用这两条不等式继续压缩。

在进行搜索的时候，把整个加法链路径进行保存，然后将路径中的每一个值都和当前节点值相加，判断是否可以是后继。如果可以，则继续搜索。

需要注意的是，在这里的搜索，要求的是小于等于，而非是平常写的小于。这是因为，路径上的其他值也会对下一次产生的节点造成影响。

本题的相关维基百科页面：[加法链](https://en.wikipedia.org/wiki/Addition_chain)

## 代码


```py
from math import log2

N = 200
log2_71 = log2(71)
f = [len(bin(k)) - 2 + bin(k).count('1') - 2 for k in range(N + 1)]
for i in range(2, N + 1):
    f[i] = min(f[i], int(4 * (len(bin(i)) - 3) / 3) + 2, int(9 / log2_71 * log2(i)))

a = [0 for _ in range(N + 1)]


def dfs(d):
    k = a[d]
    for i in range(d + 1):
        w = k + a[i]
        if w <= N:
            if d + 1 <= f[w]:
                a[d + 1] = w
                f[w] = d + 1
                dfs(d + 1)
        else:
            break


a[0] = 1
dfs(0)
ans = sum(f[1:])
print(ans)

```