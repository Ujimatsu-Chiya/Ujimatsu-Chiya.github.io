---
title: Project Euler 209
tags:
  - Project Euler
  - 动态规划
mathjax: true
date: 2022-06-02 21:04:02
---

<escape><!-- more --></escape>

# Project Euler 209

## 题目

### Circular Logic

A $k$-input *binary truth table* is a map from $k$ input bits(binary digits, $0$ [false] or $1$ [true]) to $1$ output bit. For example, the $2$-input binary truth tables for the logical $\text{AND}$ and $\text{XOR}$ functions are:

|$x$|$y$|$x \text{ AND } y$||$x$|$y$|$x \text{ XOR }  y$|
|-|-|-|-|-|-|-|
|$0$|$0$|$0$||$0$|$0$|$0$|
|$0$|$1$|$0$||$0$|$1$|$1$|
|$1$|$0$|$0$||$1$|$0$|$1$|
|$1$|$1$|$1$||$1$|$1$|$0$|

How many $6$-input binary truth tables, $\tau$, satisfy the formula

$$\tau(a, b, c, d, e, f) \text{ AND } τ(b, c, d, e, f, a \text{ XOR } (b \text{ AND } c)) = 0 $$

for all $6$-bit inputs $(a, b, c, d, e, f)$?

## 解决方案

设一个$6$位二进制数$b=b_5b_4b_3b_2b_1b_0$表示$\tau$函数的$6$个输入位$\tau(b_0,b_1,b_2,b_3,b_4,b_5)$。

根据题目中的定义，对于$\forall b\in \{0,1\}^6$，上面的式子中的两个$\tau$必须有一个为$0$。

我们枚举了$64$个不同的输入，根据上面的公式，发现它们组成了一个个环，这些环一共有$6$个，分别如下（以下分别表示$b$的值）：

$\begin{aligned}
& 0\leftrightarrow0\\
&1\leftrightarrow32\leftrightarrow16\leftrightarrow8\leftrightarrow4\leftrightarrow2\leftrightarrow1\\
&3\leftrightarrow33\leftrightarrow48\leftrightarrow24\leftrightarrow12\leftrightarrow6\leftrightarrow35\leftrightarrow49\leftrightarrow56\leftrightarrow28\leftrightarrow14\leftrightarrow39\leftrightarrow19\leftrightarrow41\leftrightarrow52\leftrightarrow26\\&
\leftrightarrow13\leftrightarrow38\leftrightarrow51\leftrightarrow57\leftrightarrow60\leftrightarrow30\leftrightarrow47\leftrightarrow23\leftrightarrow11\leftrightarrow37\leftrightarrow50\leftrightarrow25\leftrightarrow44\leftrightarrow22\leftrightarrow43\\&
\leftrightarrow53\leftrightarrow58\leftrightarrow29\leftrightarrow46\leftrightarrow55\leftrightarrow27\leftrightarrow45\leftrightarrow54\leftrightarrow59\leftrightarrow61\leftrightarrow62\leftrightarrow63\leftrightarrow31\leftrightarrow15\leftrightarrow7\leftrightarrow3\\
&5\leftrightarrow34\leftrightarrow17\leftrightarrow40\leftrightarrow20\leftrightarrow10\leftrightarrow5\\
& 9\leftrightarrow36\leftrightarrow18\leftrightarrow9\\
& 21\leftrightarrow42\leftrightarrow21
\end{aligned}$

这些环中的相邻两个输入在$\tau$的真值表其中必须其中一个是$0$。并且，不同环之间是相互独立的，因此将每个环的填法数相乘就是最终答案。这引出第二个问题：

给定一个长度为$n$的**环形**数组，数组的值只能填$0$或$1$。有多少种填法，使得环形数组不能存在相邻两个值为$1$？

这个问题可以使用动态规划方便地解决，假设所求的值为$f(n)$，那么可以写出如下状态转移方程：
$$
f(i)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=1 \\
  &3 & & \mathrm{else if\quad} i=2 \\
  &f(i-1)+f(i-2) & & \mathrm{else}
\end{aligned}\right.
$$

由于是一个环形数组，因此考虑在第$1$位和最后一位之间插入新的值。对于$f(n-1)$的情形，只需要插入一个$0$即可。对于$f(n-2)$的情形，那么就有以下情况考虑：

1. 第$1$位和第$n-2$位都为$0$，那么插入一个"$01$"。（如果插入"$10$"，那么会和$f(n-1)$的情况重复）
2. 第$1$位为$0$，第$n-2$位为$1$，那么插入一个"$01$"。
3. 第$1$位为$1$，第$n-2$位为$0$，那么插入一个"$10$"。

这$3$种情况，对于$f(n-2)$中的任意一种情况，总是符合上面$3$种情况之一，进行对应的转移，因此都包含在$f(n-2)$中。

这$6$个环的长度分别为$1,6,46,6,3,2$，因此答案为$f(1)\cdot f(6)\cdot f(46)\cdot f(6)\cdot f(3)\cdot f(2)$

## 代码

```py
M = 6
f = [-1, 1, 3]
for i in range(1 << M):
    f.append(f[-1] + f[-2])
st = set()
ans = 1
for s in range(1 << M):
    if s in st:
        continue
    st.add(s)
    cnt = 1
    while True:
        s = s >> 1 | (s & 1 ^ ((s >> 1) & (s >> 2) & 1)) << 5
        if s in st:
            break
        cnt += 1
        st.add(s)
    ans *= f[cnt]
print(ans)

```
