---
title: Project Euler 622
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 622
## 题目
### Riffle Shuffles



A riffle shuffle is executed as follows: a deck of cards is split into two equal halves, with the top half taken in the left hand and the bottom half taken in the right hand. Next, the cards are interleaved exactly, with the top card in the right half inserted just after the top card in the left half, the $2\text{nd}$ card in the right half just after the $2\text{nd}$ card in the left half, etc. (Note that this process preserves the location of the top and bottom card of the deck)


Let $s(n)$ be the minimum number of consecutive riffle shuffles needed to restore a deck of size $n$ to its original configuration, where $n$ is a positive even number.

Amazingly, a standard deck of $52$ cards will first return to its original configuration after only $8$ perfect shuffles, so $s(52) = 8$. It can be verified that a deck of $86$ cards will also return to its original configuration after exactly $8$ shuffles, and the sum of all values of $n$ that satisfy $s(n) = 8$ is $412$.


Find the sum of all values of $n$ that satisfy $s(n) = 60$.


## 解决方案

结论：洗$2n$张牌，恢复到原来的步骤数等于元素$2$在群$\mathbb{Z}_{2n-1}^{\star}$上的阶$\lambda_{2n-1}(2)$。

说明：将$2n$张牌从小到大标记成数字$0\sim 2n-1$，牌的位置也标记成$0\sim 2n-1$，那么洗完一次牌后，第$0<i<n$张牌的位置将会到达$2i$。因为第$i$张牌前面都多了$i$张右边的牌。而第$n\le j<2n-1$张牌就到达了第$2j\%(2n-1)$的位置。

因此综上所述，第$i$张一轮完成后就到达了位置$2i\%(2n-1)$，两轮完成后就是位置$2\cdot 2i\%(2n-1)$，三轮完成后就是$2^3i\%(2n-1)$……$k$轮完成后就是$2^ki\%(2n-1)$。因此，最终所有牌如果需要回到原来的位置，那么洗牌的最小轮数$k$就必须满足$2^k\equiv1 (\mod 2n-1)$，也就是元素$2$在群$\mathbb{Z}_{2n-1}^{\star}$上的阶$\lambda_{2n-1}(2)$。这说明$2n-1|2^k-1$.

令$N=60$。那么这我们可以枚举出$2^N-1$的所有因数$d$，然后再进一步判断$\lambda_{d}(2)$的值是否为$N$即可。如果是$N$，那么$d+1$就为所需要的答案。


## 代码


```py
from sympy import n_order
from tools import divisors

N = 60
ans = sum((d+1) for d in divisors(2 ** N - 1) if n_order(2, d) == N)
print(ans)

```