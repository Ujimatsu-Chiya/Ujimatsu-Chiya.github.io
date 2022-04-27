---
title: Project Euler 19
tags:
  - Project Euler
mathjax: true
date: 2022-04-27 09:55:50
---

<escape><!-- more --></escape>

# Project Euler 19
## 题目
### Counting Sundays

You are given the following information, but you may prefer to do some research for yourself.
- $1$ Jan $1900$ was a Monday.
- Thirty days has September,
April, June and November.
All the rest have thirty-one,
Saving February alone,
Which has twenty-eight, rain or shine.
And on leap years, twenty-nine.
 - A leap year occurs on any year evenly divisible by 4, but not on a century unless it is divisible by 400.

How many Sundays fell on the first of the month during the twentieth century ($1$ Jan $1901$ to $31$ Dec $2000$)?

## 解决方案

可以使用Python中datetime包的date类解决。

## 代码

```py
from datetime import date

l = 1901
r = 2000
ans = 0
for y in range(l, r + 1):
    for m in range(1, 13):
        if date(y, m, 1).isoweekday() == 7:
            ans += 1
print(ans)
```