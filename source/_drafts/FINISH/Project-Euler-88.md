---
title: Project Euler 88
tags:
  - Project Euler
  - OEIS
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 88
## 题目
### Product-sum numbers



A natural number, $N$, that can be written as the sum and product of a given set of at least two natural numbers, $\{a_1, a_2, ... , a_k\}$ is called a product-sum number: $N = a_1 + a_2 + ... + a_k = a_1 \times a_2 \times ... \times a_k$.
For example, $6 = 1 + 2 + 3 = 1 \times 2 \times 3$.
For a given set of size, $k$, we shall call the smallest $N$ with this property a minimal product-sum number. The minimal product-sum numbers for sets of size, $k = 2, 3, 4, 5$, and $6$ are as follows.
$k=2:4=2 \times 2 = 2 + 2$
$k=3:6=1 \times 2 \times 3 = 1 + 2 + 3$
$k=4:8=1 \times 1 \times 2 \times 4 = 1 + 1 + 2 + 4$
$k=5:8=1 \times 1 \times 2 \times 2 \times 2  = 1 + 1 + 2 + 2 + 2$
$k=6:12=1 \times 1 \times 1 \times 1 \times 2 \times 6 = 1 + 1 + 1 + 1 + 2 + 6$

Hence for $2\leq k\leq 6$, the sum of all the minimal product-sum numbers is $4+6+8+12=30;$ note that $8$ is only counted once in the sum.

In fact, as the complete set of minimal product-sum numbers for $2\leq k\leq 12$ is $\{4, 6, 8, 12, 15, 16\}$, the sum is $61$.

What is the sum of all the minimal product-sum numbers for $2\leq k\leq12000$?

## 解决方案

可以知道，对于绝大多数$k$，满足题目条件的序列$\{a\}$中，大多数的值都是$1$，最多只有$m=\lfloor\log_2k\rfloor$个数的值非$1$。

因此，不失一般性，先对$\{a\}$（长度未知）的前$m$个的值进行枚举，那么最终可以计算出长度$k=\prod_{i=1}^m-\sum_{i=1}^ma_i+m$，其余$k-m$个值必定全为$1$。

为了遍历所有情况，本代码遍历时，$a_1,a_2,...,a_m$可以为$1$，这是为了方便求出$k$比较小时的情况。

关于在某个特定的$k$下，和积值$N$的上限.先枚举前几项出来，查询OEIS的结果为[A104173](https://oeis.org/A104173)。在FORMULA一栏，发现：
```
a(n) <= 2n, since 1^(n-2)* 2*n = (n-2)*1 + 2 + n. - Étienne Dupuis, Dec 07 2021
```
这说明，每个答案的上限不会超过$2k$。

因此，直接搜索前$m$个值即可，途中需要记录这$m$个值的和与积，这些积值不需要超过$2N$。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N=12000;
const int M=log2(1e-8+N);
int f[N+4];
void dfs(int fl, int pre, int mul, int sum) {
    if (fl == M) {
        int t = mul - sum + M;
        if (t <= N)
            f[t] = min(f[t], mul);
        return;
    }
    for (int i = pre; i <= N && mul * i <= N * 2; i++)
        dfs(fl + 1, i, mul * i, sum + i);
}
int main(){
    memset(f,0x3f,sizeof(f));
    f[2]=4;
    dfs(0,1,1,0);
    unordered_set<int>st;
    for(int i=2;i<=N;i++)
        st.insert(f[i]);
    int ans=0;
    for(int x:st)
        ans+=x;
    printf("%d\n",ans);
}

```