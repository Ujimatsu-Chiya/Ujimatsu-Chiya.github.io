---
title: Project Euler 813
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 813
## 题目
### XOR-Powers


We use $x\oplus y$ to be the bitwise XOR of $x$ and $y$.

Define the *XOR-product* of $x$ and $y$, denoted by $x \otimes y$, similar to a long multiplication in base $2$, except that the intermediate results are XORed instead of the usual integer addition.

For example, $11 \otimes 11 = 69$, or in base $2$, $1011_2 \otimes 1011_2 = 1000101_2$:
$$
\begin{align*}
\phantom{\otimes 1111} 1011_2 \\
\otimes \phantom{1111} 1011_2 \\
\hline
\phantom{\otimes 1111} 1011_2 \\
\phantom{\otimes 111} 1011_2 \phantom{9} \\
\oplus \phantom{1} 1011_2  \phantom{999} \\
\hline
\phantom{\otimes 11} 1000101_2 \\
\end{align*}
$$
Further we define $P(n) = 11^{\otimes n} = \overbrace{11\otimes 11\otimes \ldots \otimes 11}^n$. For example $P(2)=69$.

Find $P(8^{12}\cdot 12^8)$. Give your answer modulo $10^9+7$.

## 解决方案

令$n=8^{12}\cdot 12^8$。

将二进制数$1011_{2}$视为一个用异或加法表示的多项式$1\oplus x\oplus x^3$。那么可以发现，将这个多项式对自身相乘，可以得到新的多项式为$1\oplus x^2\oplus x^6$。将得出来的多项式$1\oplus x^2\oplus x^6$再与自身相乘，那么可以得到$1\oplus x^4\oplus x^{12}$。

由此可以发现规律：$11^{\otimes 2^n}$可以表示成多项式$1\oplus x^{2^n}\oplus x^{3\cdot 2^n}$。也就是说，$P(2^n)=1+2^{2^n}+2^{3\cdot2^n}$。

不难发现，函数$P$满足此性质$P(a+b)=P(a)\otimes P(b)$。因此我们可以把$n$拆分成一个个二进制幂之和，然后再利用这个运算性质，直接将$P(a)$和$P(b)$对应的多项式直接卷积进行计算即可。

## 代码

```py
N = 12 ** 8 * 8 ** 12
mod = 10 ** 9 + 7


def conv(sa, sb):
    from collections import defaultdict
    mp = defaultdict(int)
    for x in sa:
        for y in sb:
            mp[x + y] ^= 1
    return {k for k, v in mp.items() if v}


su = {0}
st = {0, 1, 3}
while N:
    if N & 1:
        su = conv(su, st)
    st = conv(st, st)
    N >>= 1
ans = sum(pow(2, x, mod) for x in su) % mod
print(ans)

```