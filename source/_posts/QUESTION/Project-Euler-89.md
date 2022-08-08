---
title: Project Euler 89
category:
  - Project Euler
tags:
  - 模拟
  - 贪心
mathjax: true
date: 2022-04-26 16:10:19
---


<escape><!-- more --></escape>

# Project Euler 89

## 题目

### Roman numerals

For a number written in Roman numerals to be considered valid there are basic rules which must be followed. Even though the rules allow some numbers to be expressed in more than one way there is always a “best” way of writing a particular number.
For example, it would appear that there are at least six ways of writing the number sixteen:

<span style="font-family:courier new,monospace;">IIIIIIIIIIIIIIII</span> </br><span style="font-family:courier new,monospace;">VIIIIIIIIIII</span> </br><span style="font-family:courier new,monospace;">VVIIIIII</span> </br><span style="font-family:courier new,monospace;">XIIIIII</span></br><span style="font-family:courier new,monospace;">VVVI</span> </br><span style="font-family:courier new,monospace;">XVI</span></br>

However, according to the rules only <span style="font-family:courier new,monospace;">XIIIIII</span> and <span style="font-family:courier new,monospace;">XVI</span> are valid, and the last example is considered to be the most efficient, as it uses the least number of numerals.

The 11K text file, [roman.txt](../resources/p089_roman.txt) (right click and ‘Save Link/Target As…’), contains one thousand numbers written in valid, but not necessarily minimal, Roman numerals; see <a href="https://projecteuler.net/about=roman_numerals" target="_blank" rel="noopener">About… Roman Numerals</a> for the definitive rules for this problem.

Find the number of characters saved by writing each of these in their minimal form.
Note: You can assume that all the Roman numerals in the file contain no more than four consecutive identical units.

## 解决方案

根据罗马数字的规则，可以先把所有字母对应的数直接全部用字典存。

不过，罗马数字处理减法规则时可能有点麻烦。为解决这个困难，本代码使用的方案是将所有减法规则当作一个“标记”，也存在字典中。

对罗马数进行解析的时候，需要先判断当前字母有没有应用到减法规则。如果有，那就和下一个字母一起计算，否则单独计算。

将整数转化成罗马数的时候，对应使用贪心思想，每次取最大的进行拼接即可。

## 代码

```py
ls = open('p089_roman.txt', 'r').readlines()
mp = {
    'IV': 4, 'IX': 9, 'XL': 40, 'XC': 90, 'CD': 400, 'CM': 900,
    'M': 1000, 'D': 500, 'C': 100, 'L': 50, 'X': 10, 'V': 5, 'I': 1
}
ln = []
for x, y in mp.items():
    ln.append([y, x])
ln.sort()
ln.reverse()


# 将一个任意形式的罗马数转化为整数。
def r2n(s: str):
    ans = 0
    while s != "":
        if len(s) >= 2 and s[0:2] in mp.keys():
            ans += mp[s[0:2]]
            s = s[2:]
        else:
            ans += mp[s[0]]
            s = s[1:]
    return ans


# 将一个整数转化为有效的罗马数。
def n2r(n: int):
    s = ""
    for x, y in ln:
        cnt = n // x
        s += y * cnt
        n -= x * cnt
    return s

ans = 0
for s in ls:
    s = s.replace('\n', '')
    ans += len(s) - len(n2r(r2n(s)))
print(ans)

```
