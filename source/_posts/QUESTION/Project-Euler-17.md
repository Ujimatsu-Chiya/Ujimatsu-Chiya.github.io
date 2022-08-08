---
title: Project Euler 17
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-27 09:55:41
---

<escape><!-- more --></escape>

# Project Euler 17

## 题目

### Number letter counts

If the numbers $1$ to $5$ are written out in words: one, two, three, four, five, then there are $3 + 3 + 5 + 4 + 4 = 19$ letters used in total.

If all the numbers from $1$ to $1000$ (one thousand) inclusive were written out in words, how many letters would be used?

**NOTE:** Do not count spaces or hyphens. For example, $342$ (three hundred and forty-two) contains $23$ letters and $115$ (one hundred and fifteen) contains $20$ letters. The use of "and" when writing out numbers is in compliance with British usage.

## 解决方案

本代码分四种情况：

$0\sim20$：直接记录在字典中，直接获得即可。

$21~99$：计算出十位和个位的结果，然后直接相加。个位为$0$的情况下，不需要添加。

所有$0\sim100$的情况将存在另一个字典中。

$100\sim999$：将数拆成百位和(十位个位)两部分，需要注意用到"hundred"和"and"的情况。

$1000$：直接写死。

## 代码

```Python
mp = {
    0: "",
    1: "one",
    2: "two",
    3: "three",
    4: "four",
    5: "five",
    6: "six",
    7: "seven",
    8: "eight",
    9: "nine",
    10: "ten",
    11: "eleven",
    12: "twelve",
    13: "thirteen",
    14: "fourteen",
    15: "fifteen",
    16: "sixteen",
    17: "seventeen",
    18: "eighteen",
    19: "nineteen",
    20: "twenty",
    30: "thirty",
    40: "forty",
    50: "fifty",
    60: "sixty",
    70: "seventy",
    80: "eighty",
    90: "ninety",
    100: "hundred",
    1000: "one thousand",
}
# 提前记录1000的结果。
ans = len(mp[1000]) - 1
mq = {}
for i in range(1000):
    if i <= 20:
        ans += len(mp[i])
        mq[i] = len(mp[i])
    elif i < 100:
        u, v = i // 10 * 10, i % 10
        ans += len(mp[u]) + len(mp[v])
        mq[i] = len(mp[u]) + len(mp[v])
    else:
        u, v = div(i, 100)
        # hundred + 7
        ans += mq[u] + 7
        if v > 0:
            # and + 3
            ans += mq[v] + 3

print(ans)
```
