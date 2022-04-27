---
title: Project Euler 24
tags:
  - Project Euler
mathjax: true
date: 2022-04-27 09:56:11
---

<escape><!-- more --></escape>

# Project Euler 24
## 题目
### Lexicographic permutations
A permutation is an ordered arrangement of objects. For example, $3124$ is one possible permutation of the digits $1$, $2$, $3$ and $4$. If all of the permutations are listed numerically or alphabetically, we call it lexicographic order. The lexicographic permutations of $0$, $1$ and $2$ are:
$$012 \quad 021 \quad 102 \quad 120 \quad 201 \quad 210$$
What is the millionth lexicographic permutation of the digits $0$, $1$, $2$, $3$, $4$, $5$, $6$, $7$, $8$ and $9$?
## 解决方案
使用[康托逆展开](https://baike.baidu.com/item/%E5%BA%B7%E6%89%98%E5%B1%95%E5%BC%80/7968428?fr=aladdin)。

基本思想是，假设这是一个$n$阶置换。在本问题下，如果现在在填第$i(i$的下标从$0$开始$)$个数，那么后面还有$n-i-1$个数，这$n-i-1$个数全排列一共有$(n-i-1)!$种情况。并且，无论填哪个数，后面都是$(n-i-1)!$种的情况。因此，用当前字典序排名整除值$(n-i-1)!$，可以计算出当前目前的所需要填的值的排名。将这个值填充到第$i$个位置后，需要删除。接下来就一直往后解决该子结果下的新子问题。
## 代码

```python
Q = 10 ** 6
Q -= 1
N = 10
a = [i for i in range(N)]
b = []
for i in range(N):
    p, now = divmod(Q, fac(N - i - 1))
    b.append(a[p])
    del a[p]
    Q = now
print("".join(str(x) for x in b))
```