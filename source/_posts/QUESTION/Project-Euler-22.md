---
title: Project Euler 22
tags:
  - Project Euler
mathjax: true
date: 2022-04-25 10:44:10
---


<escape><!-- more --></escape>

# Project Euler 22

## 题目

### Names score

Using [names.txt](../resources/p022_names.txt) (right click and ‘Save Link/Target As…’), a 46K text file containing over five-thousand first names, begin by sorting it into alphabetical order. Then working out the alphabetical value for each name, multiply this value by its alphabetical position in the list to obtain a name score.

For example, when the list is sorted into alphabetical order, COLIN, which is worth $3 + 15 + 12 + 9 + 14 = 53$, is the $938$th name in the list. So, COLIN would obtain a score of $938 \times 53 = 49714$.

What is the total of all the name scores in the file?

## 解决方案

将读入的字符串用一个列表存下。然后直接排序，直接计算相加得到结果。

## 代码

```py
ls = open('p022_names.txt', 'r').readlines()[0].split(',')
ls.sort()
ans = 0
for i in range(len(ls)):
    s = ls[i].replace("\"", "")
    val = 0
    for ch in s:
        val += ord(ch) - ord('A') + 1
    ans += val * (i + 1)
print(ans)
```
