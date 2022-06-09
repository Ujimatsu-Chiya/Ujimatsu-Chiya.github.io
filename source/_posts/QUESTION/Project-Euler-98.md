---
title: Project Euler 98
tags:
  - Project Euler
mathjax: true
date: 2022-04-30 10:33:04
---

<escape><!-- more --></escape>

# Project Euler 98

## 题目

### Anagramic squares

By replacing each of the letters in the word CARE with $1, 2, 9$, and $6$ respectively, we form a square number: $1296 = 36 ^2$. What is remarkable is that, by using the same digital substitutions, the anagram, RACE, also forms a square number: $9216 = 96 ^2$. We shall call CARE (and RACE) a square anagram word pair and specify further that leading zeroes are not permitted, neither may a different letter have the same digital value as another letter.

Using [words.txt](../resources/p098_words.txt) (right click and 'Save Link/Target As...'), a 16K text file containing nearly two-thousand common English words, find all the square anagram word pairs (a palindromic word is NOT considered to be an anagram of itself).

What is the largest square number formed by any member of such a pair?

NOTE: All anagrams formed must be contained in the given text file.

## 解决方案

先进行两步预处理。

1. 首先将所有同构的字符串放在一起，再将这些同构的字符串对处理出来。可以发现，数量大于$1$的类别很少。因此，经过这次预处理，同构字符串对的数量很少。
2. 将所有存在自身的排列也是平方数的平方数（如$144$和$441$）按照使用数位的情况分类进行存储。类似的，可以发现，数量大于$1$的类别也很少。

这次预处理则将大量平方数和大量字符串进行排除，方便后面筛选。

接下来，对所有同构的字符串对进行枚举。
遍历对应长度下的所有平方数，尝试按照两个同构字符串的方式，将这个平方数映射成另外一个数。最后判断答案合法性即可。

## 代码

```py
ls = open('p098_words.txt', 'r').readlines()[0].split(',')


# 判断两个字符串是否同构。
def cmp(s: str, t: str):
    m = len(s)
    for i in range(m):
        for j in range(i + 1, m):
            if (s[i] == s[j]) ^ (t[i] == t[j]):
                return 0
    return 1


# 输入一个字符串s和其同构的字符串数t，返回s依照w对t进行重排的数。
def replace(s: str, t: str, w: str):
    m = len(s)
    my_mp = {}
    for i in range(m):
        my_mp[s[i]] = t[i]
    z = ""
    for i in range(m):
        z += my_mp[w[i]]
    return int(z)


# 预处理出pairs，所有的重排单词对。
mp, pairs = {}, []
for s in ls:
    s = s[1:-1]
    u = "".join((lambda x: (x.sort(), x)[1])(list(s)))
    if u not in mp.keys():
        mp[u] = []
    mp[u].append(s)
mx_str_len = 0
for y in mp.values():
    if len(y) >= 2:
        m = len(y)
        for i in range(m):
            mx_str_len = max(mx_str_len, len(y[i]))
            for j in range(i + 1, m):
                pairs.append([y[i], y[j]])
# print(len(pairs))
mp, mq = {}, {}
i = 1
while True:
    x = i * i
    if x >= 10 ** mx_str_len:
        break
    s = str(x)
    u = "".join((lambda x: (x.sort(), x)[1])(list(s)))
    if u not in mp.keys():
        mp[u] = []
    mp[u].append(x)
    i += 1

for y in mp.values():
    if len(y) >= 2:
        for w in y:
            l = len(str(w))
            if l not in mq.keys():
                mq[l] = set()
            mq[l].add(w)

ans = 0
for x, y in pairs:
    m = len(x)
    if m not in mq.keys():
        continue
    for val in mq[m]:
        # 不同字母必须对应不同数字。因此x和str(val)需要同构。
        if cmp(x, str(val)) and replace(x, str(val), y) in mq[m]:
            ans = max(ans, val, replace(x, str(val), y))
print(ans)
```
