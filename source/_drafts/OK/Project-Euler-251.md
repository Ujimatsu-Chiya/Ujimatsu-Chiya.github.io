---
title: Project Euler 251
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    



# Project Euler 251
## 题目
### Cardano Triplets

A triplet of positive integers $(a,b,c)$ is called a Cardano Triplet if it satisfies the condition:

$$\sqrt[3]{a + b \sqrt{c}} + \sqrt[3]{a - b \sqrt{c}} = 1$$

For example, $(2,1,5)$ is a Cardano Triplet.

There exist $149$ Cardano Triplets for which $a+b+c \le 1000$.

Find how many Cardano Triplets exist such that $a+b+c \le 110,000,000$.


## 解决方案

先将整个方程去除根号：

1. 等式两边立方，整理后得

$$2a+3\sqrt[3]{a^2-b^2c}\cdot(\sqrt[3]{a + b \sqrt{c}} + \sqrt[3]{a - b \sqrt{c}})=1$$

2. 代入原来的$\sqrt[3]{a + b \sqrt{c}} + \sqrt[3]{a - b \sqrt{c}}=1$，移项后，整理得：

$$2a-1=-3\sqrt[3]{a^2-b^2c}$$

3. 等式两边再取立方，整理后得：

$$8a^3+15a^2+6a-1=27b^2c\qquad(1)$$

原式等价于求$8a^3+15a^2+6a-1=27b^2c$的解。

左边的式子可以分解为$(a+1)^2(8a-1)$，不难发现，只有当$a$满足$a\equiv 2(\mod 3)$时，$3|(a+1)^2(8a-1)$。

因此，令$a=3k+2,k\ge0$，将此式代回$(1)$，整理后，问题转化为求有多少个三元组$(k,b,c)$，满足以下方程：

$$(k+1)^2(8k+5)=b^2c\qquad (2)$$

其中，$k\ge0,b>0,c>0,3k+2+b+c\le N,N=110000000$。

观察到$(2)$两侧都是一个平方项乘以一个一次项，令$g=\gcd(k+1,b)$，那么令$p,q$满足$k+1=gp,b=gq$，其中$\gcd(p,q)=1$。那么将$p,q$代入$(2)$，有

$$p^2(8k+5)=q^2c\qquad(3)$$

由于$\gcd(p,q)=1$，因此存在$m$，使得$c=mp^2,8k+5=mq^2$。

联立$a=3k+2,b=gq,c=mp^2,k+1=gp,8k+5=mq^2$，可将问题转化为如下形式：
有多少个整数三元组$(a=3gp+1,b=gq,c=mp^2)$满足以下条件：

1. $\gcd(p,q)=1$
2. $8gp=mq^2+3$
3. $3gp+1+gq+mp^2\le N$

我们可以枚举每对互质的$(p,q)$后开始统计。

## 代码


```py
N = 110000000
M = (N + 1) // 3
MXR = int((((M * 8) - 3) / 5) ** 0.5)
MXQ = int(((N + 1) / 5) ** 0.5)


def ex_gcd(a: int, b: int):
    if b == 0:
        return 1, 0, a
    else:
        x, y, g = ex_gcd(b, a % b)
        return y, x - (a // b) * y, g


def solve_ax_plus_by_is_c(a: int, b: int, c: int):
    if a < 0:
        a, b, c = -a, -b, -c
    x, y, g = ex_gcd(a, b)
    if c % g != 0:
        return None
    ma = abs(a // g)
    mc = c // g
    x *= mc
    y *= mc
    y = (y % ma + ma) % ma
    x = (c - b * y) // a
    return x, y, abs(g)


ans = 0
for r in range(1, MXR + 1, 2):
    for q in range(1, MXQ + 1):
        v = solve_ax_plus_by_is_c(8 * q, -r * r, 3)
        if v is None or v[2] != 1:
            continue
        p, s, g = v
        low = p * r + s * q * q + p * 3 * q
        # print(q, r, 8 * r, q * q, p, s, low)
        d = r * r * (r + (3 * q)) + 8 * q ** 3
        if low > N + 1:
            continue
        elif low + d > N + 1:
            ans += 1
        else:
            ans += 1 + (N + 1 - low) // d
print(ans)
'''
原式等价于求8*a^3+15*a^2+6a-1=27b^2c的解。
令F(a)=8*a^3+15*a^2+6a-1。
可知，当a%3==2时，F(a)%27==0。
F(a)分解因式后为(a+1)^2(8a-1)。
令a=3k+2，k>=0，则G(k)=F(3k+2)=27(k+1)^2(8k+5)。
即求(k+1)^2(8k+5)=b^2c[A]的所有解，且3k+2+b+c<=M
设p=gcd(b,k+1)，那么就可以写成b=pr和k+1=pq，其中gcd(r,q)=1。
代入[A]，则有cr^2=q^2(8k+5)[B]。
由于r和q互质，因此存在s使得c=sq^2且8k+5=sr^2。
联立b=pr,c=sq^2,k+1=pq和8k+5=sr^2。
问题转化成三元组(a=3pq-1, b=pr, c=sq^2)中，满足下面条件的个数：
1. gcd(r,q)=1.
2. 8pq=sr^2+3.
3. 3pq+pr+sq^2<=M+1.
枚举每对互质的(q,r)后开始计算。
也可以知道，如果存在最小的P和S满足方程8Pq=Sr^2+3，那么p'=P+r^2，s'=S+8q也是方程的解。
所以问题则转化为计算有多少个k使得k>=0且3pq+pr+sq^2<=M+1。代入后，即P(3q+r)+Sq^2+k(r^2(3q+r)+8q^3)<=M+1。
P和S的值可以通过扩展欧几里德算法计算。
'''
```