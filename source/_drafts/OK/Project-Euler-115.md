---
title: Project Euler 115
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 115
## 题目
### Counting block combinations II


NOTE: This is a more difficult version of <a href="/Problem101-125/#Problem_114">Problem 114</a>.

A row measuring $n$ units in length has red blocks with a minimum length of $m$ units placed on it, such that any two red blocks (which are allowed to be different lengths) are separated by at least one black square.

Let the fill-count function, $F(m, n)$, represent the number of ways that a row can be filled.

For example, $F(3, 29) = 673135$ and $F(3, 30) = 1089155$.
That is, for $m = 3$, it can be seen that $n = 30$ is the smallest value for which the fill-count function first exceeds one million.

In the same way, for $m = 10$, it can be verified that $F(10, 56) = 880711$ and $F(10, 57) = 1148904$, so $n = 57$ is the least value for which the fill-count function first exceeds one million.

For $m = 50$, find the least value of $n$ for which the fill-count function first exceeds one million.


## 解决方案

使用的方案和第114题完全相同，此处不赘述。

## 代码

```py
from itertools import count

Q = 10 ** 6
M = 50
f = [1]
g = [0]
s = [1]
for i in count(1, 1):
    f.append(f[i - 1] + g[i - 1])
    g.append(0 if i < M else s[i - M])
    s.append(s[i - 1] + f[i])
    if f[i] + g[i] > Q:
        ans = i
        break
print(ans)

```

