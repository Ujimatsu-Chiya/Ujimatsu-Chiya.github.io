---
title: Project Euler 523
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-07-13 22:57:20
---

<escape><!-- more --></escape>

# Project Euler 523

## 题目

### First Sort I

Consider the following algorithm for sorting a list:

1. Starting from the beginning of the list, check each pair of adjacent elements in turn.
2. If the elements are out of order:
a. Move the smallest element of the pair at the beginning of the list.
b. Restart the process from step 1.
3. If all pairs are in order, stop.

For example, the list $\{4\ 1\ 3\ 2\}$ is sorted as follows:

- <u>4 1</u> 3 2  ($4$ and $1$ are out of order so move $1$ to the front of the list)
- 1 <u>4 3</u> 2  ($4$ and $3$ are out of order so move $3$ to the front of the list)
- <u>3 1</u> 4 2  ($3$ and $1$ are out of order so move $1$ to the front of the list)
- 1 3 <u>4 2</u>  ($4$ and $2$ are out of order so move $2$ to the front of the list)
- <u>2 1</u> 3 4  ($2$ and $1$ are out of order so move $1$ to the front of the list)
- 1 2 3 4  (The list is now sorted)

Let $F(L)$ be the number of times step 2a is executed to sort list $L$. For example, $F(\{ 4\ 1\ 3\ 2 \}) = 5$.

Let $E(n)$ be the **expected value** of $F(P)$ over all permutations $P$ of the integers $\{1, 2, \dots, n\}$.

You are given $E(4) = 3.25$ and $E(10) = 115.725$.

Find $E(30)$. Give your answer rounded to two digits after the decimal point.

## 解决方案

对于一个$n$阶排列，只有当前$n-1$个元素有序时，第$n$个元素才会被题目所描述的算法遍历到。并且，使前$n-1$个元素有序，花费的期望可以视为$n-1$阶排列的子问题，为$E(n-1).$

前$n-1$个数有序后，假设第$n$个数为$k$。那么当$k=n$时，算法结束。否则，$k$将会被移到第一个位置，那么现在排列看起来形如这个样子：

$k,1,2,\dots,k-2,k-1,\mathbf{k+1},k+2,\dots,n-1,n$

那么发现$k+1,k+2,\dots,n$这一部分已经是有序的，此时只需要将这个排列$k,1,2,\dots,k-2,k-1$这一部分进行排序即可。令$f(k)$为使这个$k$阶排列有序需要迭代上面的算法次数。

将这个排列排序成$1,2,\dots,k-2,k,k-1$需要$f(k-1)$的迭代次数，因为前$k-1$个元素单独视为一个子问题。

再运行一次上面的算法，那么排列就变成$k-1,1,2,\dots,k-2,k$，完成这个排列也需要$f(k-1)$的次数。

这说明，$f(k)=2f(k)+1,f(1)=0$，因此$f(k)=2^{k-1}-1$。

那么说明，原来的$n$解排列如果以$k$为结尾，并且前$n-1$个元素已经排好序，那么仍然$f(k)+1=2^{k-1}$次排序。

$n$阶排列的末尾的元素是均匀出现的，因此有$E(n)=E(n-1)+\dfrac{1}{n}\sum_{k=1}^{n-1} 2^{k-1}$

那么化简后，得到：

$$E(n)=E(n-1)+\dfrac{2^{n-1}-1}{n}=\sum_{i=1}^n\dfrac{2^{i-1}-1}{i}$$

相关数列：[A279683](https://oeis.org/A279683)

## 代码

```py
N = 30
ans = sum((2 ** (i-1) - 1) / i for i in range(1, N + 1))
print("{:.2f}".format(ans))

```
