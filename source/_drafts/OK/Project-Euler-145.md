---
title: Project Euler 145
tags:
  - Project Euler
  - 动态规划
mathjax: true
---
<escape><!-- more --></escape>
    



# Project Euler 145
## 题目
### How many reversible numbers are there below one-billion?
Some positive integers n have the property that the sum $[ n + \mathrm{reverse}(n) ]$ consists entirely of odd (decimal) digits. For instance, $36 + 63 = 99$ and $409 + 904 = 1313$. We will call such numbers *reversible*; so $36, 63, 409$, and $904$ are reversible. Leading zeroes are not allowed in either n or reverse(n).

There are $120$ reversible numbers below one-thousand.

How many reversible numbers are there below one-billion (10^9)?


## 解决方案

首先假设$g(n)=[n+\mathrm{reverse}(n) ]$

假设$f_1(i)$满足以下条件的$i$位数$n$的个数：**无**前导$0$；$g(n)$是一个$i$位数；$g(n)$每一个数位都是奇数。

类似的，$f_2(i)$：**可能有**前导$0$；$g(n)$是一个$i$位数；$g(n)$每一个数位都是奇数。

$f_3(i)$：**无**前导$0$；$g(n)$是一个$i+1$位数；$g(n)$每一个数位都是奇数（明显加法产生进位的第$i+1$位肯定是$1$）。

$f_4(i)$：**可能有**前导0；$g(n)$是一个$i$位数；$g(n)$中高$i-1$位都是奇数，最低位则是偶数。

本题通过将为一个$i-2$位数高位前面添加一个数位$l$，低位后面添加一个数位$r$进行考虑。

如果对$f_2(i-2)$中的所有数的添加方案为：$0<l+r\le9$，$l+r$为奇数，$l,r>0$，那么就变成了$f_1(i)$中的数，每个数有$20$种添加方案；而如果是$0\le l+r\le9$，$l+r$为奇数，那么就变成了$f_2(i)$中的数，每一个数有$30$种添加方案。

如果对$f_4(i-2)$中的所有数的添加方案为：$l+r>9$，$l+r$为奇数 ，那么每个数就变成了$f_3(i)$中的数，每个数有$20$种添加方案。注意到，由于$l+r$有一个进位，那么添加后相比添加前的数有：前面的进位导致$g(n)$从$i-2$位数变成$i+1$位数，后面的进位将$g(n)$最后一位偶数$+1$变成奇数。

如果对$f_3(i-2)$中的所有数的添加方案为：$0\leq l+r<9$，$l+r$为**偶数** ，那么每个数就变成了$f_3(i)$中的数，每个数有$25$种添加方案。由于$f_3(i-2)$中的$g(n)$是$i-1$位数（最高位为$1$），因此添加的$l$就直接影响$g(n)$第$i-1$位；并且，$l+r$是一个偶数，因此添加后$g(n)$的最高位$l+r+1$是一个奇数。而$g(n)$最低位则是直接被添加了一个偶数$l+r$。

将$f_1,f_2,f_3,f_4$写成状态转移方程，有：



## 代码


