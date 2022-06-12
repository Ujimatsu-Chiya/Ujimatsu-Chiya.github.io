---
title: Project Euler 601
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 601
## 题目
### Divisibility streaks



For every positive number $n$ we define the function  $\text{streak}(n)=k$   as the smallest positive integer $k$ such that $n+k$ is not divisible by $k+1$.

E.g:<br />
$13$ is divisible by $1$ <br />
$14$ is divisible by $2$ <br />
$15$ is divisible by $3$ <br />
$16$ is divisible by $4$ <br />
$17$ is NOT divisible by $5$ <br />
So $\text{streak}(13) = 4$. <br /> 

Similarly:<br />
$120$ is divisible by $1$ <br />
$121$ is NOT divisible by $2$ <br />
So $\text{streak}(120) = 1$.


Define $P(s, N)$ to be the number of integers $n$, $1 < n < N$, for which $\text{streak}(n) = s$.

So $P(3, 14) = 1$ and $P(6, 10^6) = 14286$.


Find the sum, as $i$ ranges from $1$ to $31$, of $P(i, 4^i)$.


## 解决方案

不难发现，$k+1|n+k$当且仅当$k+1|n-1$。

那么根据$\text{streak}(n)=k$就变成了，找到一个最小的$k$，使得$k+1\nmid n-1$。这也就是说，所有$1,2,\dots,k$都能整除$n-1$，但是$k+1$不行。

可以知道，如果一个数$m$能够被$1,2,3,\dots,k$整除，那么$\text{lcm}(1,2,3,\dots,k)|m$。

令函数$L(m)=\text{lcm}(1,2,3,\dots,m)$。

那么不难确定，函数$P$的表达式为

$$P(s,N)=\lfloor\dfrac{N-1}{L(s)}\rfloor-\lfloor\dfrac{N-1}{L(s+1)}\rfloor-[s=1]$$

其中，$[]$表示示性函数，表示$[]$里面的值是否为真，如果为真，那么值为$0$，否则值为$1$。

第一项则计算出了在$1\sim N-1$中，有多少个数是$L(s)$的倍数，它们的$\text{streak}$值**大于等于**$s$。第二项则减去$L(s+1)$的倍数，它们的$\text{streak}$值**大于等于**$s+1$。那么剩下的数就确保了它们的$\text{streak}$值为$s$。第三项则避免了$1$这个答案，以符合题目中的要求。


## 代码


```py
from tools import lcm

N = 31


def P(s: int, n: int):
    n -= 1
    m = 1
    for i in range(1, s + 1):
        m = lcm(m, i)
    c1 = n // m
    if m == 1:
        c1 -= 1
    m = lcm(m, s + 1)
    c2 = n // m
    return c1 - c2


ans = 0
for i in range(1, N + 1):
    ans += P(i, 4 ** i)
print(ans)


```