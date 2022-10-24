---
title: Project Euler 42
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-27 23:32:42
---

<escape><!-- more --></escape>

# Project Euler 42

## 题目

### Coded triangle numbers

The $n^{\text{th}}$ term of the sequence of triangle numbers is given by, $t_n = \dfrac{n(n+1)}{2}$; so the first ten triangle numbers are:
$$1, 3, 6, 10, 15, 21, 28, 36, 45, 55, \dots$$

By converting each letter in a word to a number corresponding to its alphabetical position and adding these values we form a word value. For example, the word value for SKY is $19 + 11 + 25 = 55 = t_{10}$. If the word value is a triangle number then we shall call the word a triangle word.

Using [words.txt](../resources/p042_words.txt)(right click and ‘Save Link/Target As…’), a 16K text file containing nearly two-thousand common English words, how many are triangle words?

## 解决方案

先将三角形数直接添加到集合，然后计算每个单词的分值，再判断分值是否在集合中。

## 代码

```py
ls = [s[1:-1] for s in open('p042_words.txt', 'r').readlines()[0].split(',')]
st = set()
for i in range(1, 41):
    st.add(i * (i + 1) // 2)
ans = 0
for s in ls:
    sum = 0
    for c in s:
        sum += ord(c) - ord('A') + 1
    if sum in st:
        ans += 1
print(ans)
```
