---
title: Project Euler 105
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 105
## 题目
### Special subset sums: testing


Let $S(A)$ represent the sum of elements in set $A$ of size $n$. We shall call it a special sum set if for any two non-empty disjoint subsets, $B$ and $C$, the following properties are true:

1. $S(B) \neq S(C)$; that is, sums of subsets cannot be equal.
2. If $B$ contains more elements than $C$ then $S(B) > S(C)$.

For example, $\{81, 88, 75, 42, 87, 84, 86, 65\}$ is not a special sum set because $65 + 87 + 88 = 75 + 81 + 84$, whereas $\{157, 150, 164, 119, 79, 159, 161, 139, 158\}$ satisfies both rules for all possible subset pair combinations and $S(A) = 1286$.
Using [sets.txt](../resources/p105_sets.txt) (right click and "Save Link/Target As\dots"), a 4K text file with one-hundred sets containing seven to twelve elements (the two examples given above are the first two sets in the file), identify all the special sum sets,$A_1, A_2, \ldots , A_k$, and find the value of $S(A_1) + S(A_2) +\ldots + S(A_k)$.

NOTE: This problem is related to <a href="/103">Problem 103</a> and <a href="/106">Problem 106</a>.

## 解决方案

本题判断特殊子集的方法和第103题一样：

如果一个集合满足题目中的第一个条件，那么它们的所有$2^n$个子集$I$的$S(I)$都不相同。

使用反证法：设一个集合$A$，对于$A$中的两个子集$I,J$，满足$S(I)=S(J)$，有以下两种情况

1. $I \bigcap J = \emptyset$：那么明显$A$集合不符合要求。
2. $I \bigcap J \neq \emptyset$：此时取$I'=I-J,J'=J-I$，根据集合差运算的定义，有$S(I')=S(I)-S(I \bigcap J),S(J')=S(J)-S(I \bigcap J)$。可以知道，此时$I' \bigcap J' = \emptyset$，但有$S(I')=S(J')$，不符合要求。

因此原推论成立，判断集合是否为特殊不需要直接枚举一对不相交子集。而是产生所有子集，先判断元素和是否重复，然后根据和的大小进行排序比较集合大小即可（判断第二个条件是否满足）。

## 代码

```py
def ok(z: list):
    n = len(z)
    mp = {}
    for st in range(1 << n):
        cnt, s = 0, 0
        for i in range(n):
            if st >> i & 1:
                cnt += 1
                s += z[i]
        if s in mp.keys():
            return False
        mp[s] = cnt
    ls = list(mp.items())
    ls.sort()
    for i in range((1 << n) - 1):
        if ls[i][1] > ls[i + 1][1]:
            return False
    return True


ls = open('p105_sets.txt', 'r').readlines()
ans = 0
for s in ls:
    a = [int(x) for x in s.split(',')]
    if ok(a):
        ans += sum(a)
print(ans)

```