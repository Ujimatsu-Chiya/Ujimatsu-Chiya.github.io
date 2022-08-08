---
title: Project Euler 167
category:
  - Project Euler
tags:
  - 论文
  - OEIS
mathjax: true
date: 2022-05-25 18:33:21
---

<escape><!-- more --></escape>
    
    

# Project Euler 167
## 题目
### Investigating Ulam sequences
For two positive integers $a$ and $b$, the Ulam sequence $U(a,b)$ is defined by $U(a,b)_1 = a$, $U(a,b)_2 = b$ and for $k > 2,U(a,b)_k$ is the smallest integer greater than $U(a,b)_{(k-1)}$ which can be written in exactly one way as the sum of two distinct previous members of U(a,b).

For example, the sequence $U(1,2)$ begins with

$1, 2, 3 = 1 + 2, 4 = 1 + 3, 6 = 2 + 4, 8 = 2 + 6, 11 = 3 + 8;$

$5$ does not belong to it because $5 = 1 + 4 = 2 + 3$ has two representations as the sum of two previous members, likewise $7 = 1 + 6 = 3 + 4$.

Find $\sum U(2,2n+1)_k$ for $2 \leq n \leq 10$, where k = $10^{11}$.


## 解决方案

1. 这篇[文章](http://projecteuclid.org/download/pdf_1/euclid.em/1048709116)提到，形如$U(2,2n+1),n\ge 2$的乌拉姆序列，有且仅有两个项是偶数，分别为第$1$项的$2$和第$n+4$项的$4n+4$。


2. 这个[页面](https://mathworld.wolfram.com/UlamSequence.html)提到：如果乌拉姆序列中偶数的个数是有限的，那么它的差分序列**从某一个起点开始是周期性**的。

第一个问题：如何高效计算序列$U(2,2n+1)$？

不难看出，第$2$项和第$n+3$项之间的所有的奇数项是以$2n+1$为首项，$2$为公差的等差数列。

根据乌拉姆序列的定义，第$i$项$U(2,2n+1)_i$一定由序列之前的某两个项相加而成。又由于第$n+5$项及以后的所有项都是奇数，那么这些项一定是由一个奇数和一个偶数相加得出，这个偶数要么是$2$，要么是$4n+4$。因此这将帮助我们以线性阶的时间复杂度计算序列$U(2,2n+1)$：计算一个奇数$x$是否在$U(2,2n+1)$，只需要判断$x-2$和$x-(4n+4)$是否**有且仅有其中一个**在$U(2,2n+1)$中。

第二个问题：如何找到$U(2,2n+1)$的循环节，并通过循环节高效计算$U(2,2n+1)_k$？

这个问题使用了这个假设：$U(2,2n+1)$的相邻两项差值的最大值为$4n+4$。并且，这个差值在每个循环节里面出现一次。（也就是说，后一项是前一项相加$4n+4$而得，而这两项中间的其它值都不符合乌拉姆序列的定义。）

因此，我们可以枚举$U(2,2n+1)$的前多个值，如果找到了两对相邻项差值为$4n+4$，那么我们就找到了一个循环节。

需要注意，循环节的长度非常大，要开足够的数组空间。长度值表示在OEIS的[A100729](http://oeis.org/A100729)中。由于差分序列是周期性的，因此每段周期提供的差值也是一样的，这个差值在OEIS的[A100730](http://oeis.org/A100730)。

其它参考资料：[网页](https://www.sciencedirect.com/science/article/pii/009731659290042S)

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N = 10;
const ll K = 1e11;
bool vis[1<<(2*N+4)];
int ulam[1 << (2 * N + 5)];
ll cal(int n,ll m) {
    --m;
    memset(vis, 0, sizeof(vis));
    int p = 0, e1 = 2, e2 = 4 * n + 4;
    ulam[p++] = e1;
    for (int w = 2 * n + 1; w <= e2; p++, w += 2) {
        ulam[p] = w;
        vis[w >> 1] = true;
    }
    ulam[p++] = e2;
    int l, r;
    for (int i = e2 + 1, cnt = 0;; i += 2) {
        if (vis[(i - e1) >> 1] ^ vis[(i - e2) >> 1]) {
            vis[i >> 1] = true;
            ulam[p++] = i;
            if (ulam[p - 1] - ulam[p - 2] == e2) {
                ++cnt;
                if (cnt == 1) {
                    l = p - 2;
                } else {
                    r = p - 2;
                    break;
                }
            }
        }
    }
    int T = r - l;
    //打印的两个值对应A100729和A100730。
    //printf("%d %d\n", T, ulam[r] - ulam[l]);
    return m < r ? ulam[m] : max(0ll, (m - l) / T) * (ulam[r] - ulam[l]) + ulam[(m - l) % T + l];
}
int main() {
    ll ans = 0;
    for (int n = 2; n <= N; n++) {
        ans += cal(n, K);
    }
    printf("%lld\n", ans);
}
```