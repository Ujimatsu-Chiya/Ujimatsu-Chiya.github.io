---
title: Project Euler 191
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-05-19 21:57:05
---

<escape><!-- more --></escape>

# Project Euler 191

## 题目

### Prize Strings

A particular school offers cash rewards to children with good attendance and punctuality. If they are absent for three consecutive days or late on more than one occasion then they forfeit their prize.

During an $n$-day period a trinary string is formed for each child consisting of L’s (late), O’s (on time), and A’s (absent).

Although there are eighty-one trinary strings for a $4$-day period that can be formed, exactly forty-three strings would lead to a prize:

<span style="font-family:'Courier New',monospace;">
OOOO OOOA OOOL OOAO OOAA OOAL OOLO OOLA OAOO OAOA<br>
OAOL OAAO OAAL OALO OALA OLOO OLOA OLAO OLAA AOOO<br>
AOOA AOOL AOAO AOAA AOAL AOLO AOLA AAOO AAOA AAOL<br>
AALO AALA ALOO ALOA ALAO ALAA LOOO LOOA LOAO LOAA<br>
LAOO LAOA LAAO</span>

How many “prize” strings exist over a $30$-day period?

## 解决方案

本题可以使用动态规划进行解决。

假设$f(i,j)(i\ge 0,0\le j\le 2)$为长度$i$的只有O和A的字符串中，字符串最后面已经有连续$j$个A的字符串个数。

很容易列出以下状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &1 & & \text{if}\quad i=0\land j=0 \\
  &0 & & \text{else if}\quad i=0 \\
  &\sum_{k=0}^2f(i-1,k) & & \text{else if}\quad j=0 \\
  &f(i-1,j-1) & & \text{else}
\end{aligned}\right.
$$

无论什么情况，只要添加一个O，那么后面就没有连续的A了。如果添加一个A，那么连续的A的个数$j$就会增加$1$。

令$g(i)=f(i,0)+f(i,1)+f(i,2)$，那么最终答案为$g(n)+\sum_{i=1}^ng(i-1)\cdot g(n-i)$。

如果考虑上字母L，可以整合成一个$6$个状态的动态规划。在这个基础上，可以使用矩阵快速幂将整个流程加速到$O(\log n)$级别（这并非是本方案的核心内容）。[Leetcode 552](https://leetcode.cn/problems/student-attendance-record-ii/solution/xue-sheng-chu-qin-ji-lu-ii-by-leetcode-s-kdlm/)题解有对本题的更进一步的优化。

## 代码

```py
N = 30
f0, f1, f2 = 1, 0, 0
g = [1]
for i in range(1, N + 1):
    f0, f1, f2 = f0 + f1 + f2, f0, f1
    g.append(f0 + f1 + f2)
ans = g[N]
for i in range(1, N + 1):
    ans += g[i - 1] * g[N - i]
print(ans)

```
