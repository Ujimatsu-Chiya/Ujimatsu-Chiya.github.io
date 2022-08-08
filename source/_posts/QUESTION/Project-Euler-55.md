---
title: Project Euler 55
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-30 10:31:39
---

<escape><!-- more --></escape>

# Project Euler 55

## 题目

### Lychrel numbers

If we take $47$, reverse and add, $47 + 74 = 121$, which is palindromic.

Not all numbers produce palindromes so quickly. For example,

$349 + 943 = 1292$
$1292 + 2921 = 4213$
$4213 + 3124 = 7337$
That is, $349$ took three iterations to arrive at a palindrome.

Although no one has proved it yet, it is thought that some numbers, like $196$, never produce a palindrome. A number that never forms a palindrome through the reverse and add process is called a Lychrel number. Due to the theoretical nature of these numbers, and for the purpose of this problem, we shall assume that a number is Lychrel until proven otherwise. In addition you are given that for every number below ten-thousand, it will either (i) become a palindrome in less than fifty iterations, or, (ii) no one, with all the computing power that exists, has managed so far to map it to a palindrome. In fact, 10677 is the first number to be shown to require over fifty iterations before producing a palindrome: $4668731596684224866951378664$ ($53$ iterations, $28$-digits).

Surprisingly, there are palindromic numbers that are themselves Lychrel numbers; the first example is $4994$.

How many Lychrel numbers are there below ten-thousand?

NOTE: Wording was modified slightly on $24$ April $2007$ to emphasise the theoretical nature of Lychrel numbers.

## 解决方案

本题已经将上限已经圈定好迭代上限为$50$，因此如果$50$次迭代完成后仍不是回文数，那么这个数是所要求的。

因此通过Python直接进行暴力枚举迭代。

## 代码

```py
N = 10000
M = 50
ans = 0
for i in range(1, N):
    w = i
    for i in range(M):
        s = str(w)
        w = int(s) + int(s[::-1])
        s = str(w)
        if s == s[::-1]:
            break
    s = str(w)
    if s != s[::-1]:
        ans += 1
print(ans)
```
