---
title: Project Euler 201
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 201
## 题目
### Subsets with a unique sum


For any set $A$ of numbers, let $\text{sum}(A)$ be the sum of the elements of $A$.

Consider the set $B = \{1,3,6,8,10,11\}$.

There are $20$ subsets of $B$ containing three elements, and their sums are:


$\text{sum}(\{1,3,6\}) = 10$,<br />
$\text{sum}(\{1,3,8\}) = 12$,<br />
$\text{sum}(\{1,3,10\}) = 14$,<br />
$\text{sum}(\{1,3,11\}) = 15$,<br />
$\text{sum}(\{1,6,8\}) = 15$,<br />
$\text{sum}(\{1,6,10\}) = 17$,<br />
$\text{sum}(\{1,6,11\}) = 18$,<br />
$\text{sum}(\{1,8,10\}) = 19$,<br />
$\text{sum}(\{1,8,11\}) = 20$,<br />
$\text{sum}(\{1,10,11\}) = 22$,<br />
$\text{sum}(\{3,6,8\}) = 17$,<br />
$\text{sum}(\{3,6,10\}) = 19$,<br />
$\text{sum}(\{3,6,11\}) = 20$,<br />
$\text{sum}(\{3,8,10\}) = 21$,<br />
$\text{sum}(\{3,8,11\}) = 22$,<br />
$\text{sum}(\{3,10,11\}) = 24$,<br />
$\text{sum}(\{6,8,10\}) = 24$,<br />
$\text{sum}(\{6,8,11\}) = 25$,<br />
$\text{sum}(\{6,10,11\}) = 27$,<br />
$\text{sum}(\{8,10,11\}) = 29$.

Some of these sums occur more than once, others are unique.

For a set $A$, let $U(A,k)$ be the set of unique sums of $k$-element subsets of $A$, in our example we find $U(B,3) = \{10,12,14,18,21,25,27,29\}$ and $\text{sum}(U(B,3)) = 156$.

Now consider the $100$-element set $S = \{1^2, 2^2, \dots , 100^2\}$.

$S$ has $100891344545564193334812497256$ $50$-element subsets.

Determine the sum of all integers which are the sum of exactly one of the $50$-element subsets of $S$, i.e. find $\text{sum}(U(S,50))$.


## 解决方案

使用动态规划的思想解决集合的计数问题。

令$M=100,N=50,S$为$M^2$以内的最大的$N$个平方数之和。

那么，设状态$f(i,j,k)(0\le i\le M,0\le j\le \min(i,M),0\le k\le S)$表示集合$\{1^2,2^2,\dots,i^2\}$中，有多少个子集满足以下两个条件：

1. 子集的大小为$j$
2. 子集的元素和为$k$

其中，空集$\emptyset$没有使用任何元素，因此大小为$0$，元素和为$0$，作为初始状态出现。

可以列出关于$f(i,j,k)$的状态转移方程：

$$
f(i,j,k)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=0\&j=0\&k=0 \\
  &0  & & \mathrm{else if\quad} i=0 \\
  &f(i-1,j,k) & & \mathrm{else if\quad} j<i^2 \\
  &f(i-1,j,k)+f(i-1,j-1,k-i^2) & & \mathrm{else}
\end{aligned}\right.
$$

对于方程最后一行，新数$i^2$要么被使用了，就$f(i-1,j-1,k-i^2)$中的所有集合都添加一个$i^2$；要么没有被使用，直接将旧状态$f(i-1,j,k)$记录。

因此，最终答案为$\sum_{k=1}^S k\cdot[f(M,N,k)=1]$。其中，$[]$表示示性函数，表示$[]$里面的值是否为真，如果为真，那么值为$0$，否则值为$1$.

由于本题只关心$f$的值是否为$0,1$，或者是超过$2$，因此为$f$定义一个新运算$\circ$：$\{0,1,2\}^2\rightarrow\{0,1,2\}$，其中$a\circ b=\min(a+b,2)$。因此不需要计算$f$的真实值，避免了溢出问题。
## 代码


```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int M=100,N=50;
const int S=M*(M+1)*(2*M+1)/6-N*(N+1)*(2*N+1)/6;
int f[N+1][S+1];
int add[3][3];
int main() {
    f[0][0] = 1;
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            add[i][j] = min(2, i + j);
    for (int i = 1, sum = 0; i <= M; i++) {
        int v = i * i;
        sum += v;
        for (int j = min(N, i); j >= 1; j--)
            for (int k = min(S, sum); k >= v; k--)
                f[j][k] = add[f[j][k]][f[j - 1][k - v]];
    }
    ll ans = 0;
    for (int i = 1; i <= S; i++)
        if (f[N][i] == 1) ans += i;
    printf("%lld\n", ans);
}
```