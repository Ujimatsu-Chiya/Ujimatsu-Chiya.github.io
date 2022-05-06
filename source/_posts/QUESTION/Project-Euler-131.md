---
title: Project Euler 131
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:22:50
---

<escape><!-- more --></escape>
    

# Project Euler 131
## 题目
### Prime cube partnership
There are some prime values, $p$, for which there exists a positive integer, $n$, such that the expression $n^3 + n^2p$ is a perfect cube.

For example, when $p = 19, 8^3 + 8^2×19 = 12^3$.

What is perhaps most surprising is that for each prime with this property the value of $n$ is unique, and there are only four such primes below one-hundred.

How many primes below one million have this remarkable property?


## 解决方案

假设这个立方数为$m^3=n^3+n^2p$，

那么有$m^3=n^3\cdot \dfrac{n+p}{n}$

两边开立方，有$m=n\cdot \sqrt[3]{\dfrac{n+p}{n}}$

由于$m,n$都是正整数，为满足原来的式子，整个立方根表达的数必须是个有理数。

接下来证明$\gcd(n+p,n)=1$：

因为$p$是质数，如果$\gcd(n+p,n)>1$，即$\gcd(n,p)>1$，那么$n$是$p$的倍数，有$n=kp$，其中$n$是一个正整数。

回代到上面的立方数式子，得到：$m^3=(k^3+k^2)p^3$。那么，如果$(k^3+k^2)p^3$是一个立方数，那么$k^3+k^2$是一个立方数。但是，$k^3$的下一个立方数$(k+1)^3=k^3+3k^2+3k+1>k^3+k^2$。因此有：

$k^3<k^3+k^2<(k+1)^3$

这说明$k^3+k^2$夹在两个相邻立方数之间，它自己肯定不是一个立方数。因此有刚刚的结论：$\gcd(n+p,n)=1$。

因此，可以令$n+p=a^3,n=b^3$（立方根里面不需要约分），得到$p=a^3-b^3=(a-b)(a^2+ab+b^2)$。

但是，$p$是质数，但$p$却有两个因式：$a-b$和$a^2+ab+b^2$

明显观察到$a-b<a^2+ab+b^2$，所以有：$a-b=1,p=a^2+ab+b^2$。

将$b=a-1$重新代入$p=a^3-b^3$，得到$p=a^3-(a-1)^3$。因此，判断这一类数是否为质数即可。


## 代码

```py
from itertools import count

from tools import is_prime

N = 1000000
ans = 0
for i in count(1, 1):
    w = (i + 1) ** 3 - i ** 3
    if w > N:
        break
    if is_prime(w):
        ans += 1
print(ans)
```