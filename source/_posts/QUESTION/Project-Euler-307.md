---
title: Project Euler 307
category:
  - Project Euler
tags:
  - 概率
mathjax: true
date: 2022-07-06 13:08:50
---

<escape><!-- more --></escape>

# Project Euler 307

## 题目

### Chip Defects

$k$ defects are randomly distributed amongst $n$ integrated-circuit chips produced by a factory (any number of defects may be found on a chip and each defect is independent of the other defects).

Let $p(k,n)$ represent the probability that there is a chip with at least $3$ defects.

For instance $p(3,7) \approx 0.0204081633$.

Find $p(20 000, 1 000 000)$ and give your answer rounded to $10$ decimal places in the form 0.abcdefghij.

## 解决方案

不难想到先考虑事件：**全部**零件最多只有$2$个缺陷。计算出这个事件的概率后，那么这个事件的补就是题目所求的至少一个零件有$3$个缺陷。

令$K=20000,N=100000$。

枚举$i$，有$i$个零件具有两个瑕疵，那么$K-2i$个零件具有一个瑕疵，$N-K+i$个零件是没有瑕疵的。那么不难算出，这种方式一共有$\dbinom{N}{i}\cdot \dbinom{N-i}{K-2i}=\dfrac{N!}{i!(K-2i)!(N-K+i)!}$种取法。

对于瑕疵而言，相当于将$K$个瑕疵放进$i$个容量为$2$的**不同**篮子，将$K-2i$个瑕疵放进$K-2i$个容量为$1$的不同篮子的情况数。假设容量为$2$的篮子都放在容量为$1$的篮子后面，那么根据全排列数公式，可以写出$\dfrac{K!}{(2!)^i\cdot(1!)^{K-2i}}$

最终可以得到：

$$p(K,N)=1-\sum_{i=0,K-2i\le N-i}^{\min(\frac{K}{2},N)}\dfrac{1}{N^K}\cdot \dfrac{N!}{i!(K-2i)!(N-K+i)!}\cdot \dfrac{K!}{2^i} $$

注意到无论分子还是分母，数都比较大。因此考虑将它们转化成对数进行计算，在对数上计算完成后再通过幂运算转换成真正的结果。

## 代码

```C++
# include <bits/stdc++.h>
typedef long double ld;
using namespace std;
const int K=20000,N=1000000;
ld fac[N+K+2];
int main(){
    for(int i=1;i<=N+K;i++)
        fac[i]=fac[i-1]+log(i);
    ld ans=0;
    for(int i=0;i<=K/2&&i<=N;i++){
        if(K-2*i>N-i) continue;
        ld val=fac[N]+fac[K]-fac[i]-fac[K-2*i]-fac[N-K+i]-log(N)*K-log(2)*i;
        ans+=exp(val);
    }
    ans=(ld)1-ans;
    printf("%.10Lf\n",ans);
}

```
