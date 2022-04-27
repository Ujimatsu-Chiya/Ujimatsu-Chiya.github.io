---
title: Project Euler 39
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 39
## 题目
### Integer right triangles
If $p$ is the perimeter of $a$ right angle triangle with integral length sides, $\{a,b,c\}$, there are exactly three solutions for $p = 120$.
$$\{20,48,52\}, \{24,45,51\}, \{30,40,50\}$$

For which value of $p \le 1000$, is the number of solutions maximised?

## 解决方案

使用第9题时得出的结论，枚举$a$，即得到$b$的值：

$$b=\dfrac{p^2-2ap}{2(p-a)}$$

因此，直接对解进行判断。

## 代码

```py
N = 1000
mx = 0
ans = 0
for p in range(3, N + 1):
    cnt = 0
    for a in range(1, p // 3 + 1):
        if (p * p - 2 * a * p) % (2 * p - 2 * a) == 0:
            b = (p * p - 2 * a * p) // (2 * p - 2 * a)
            c = p - a - b
            if a < b < c:
                cnt += 1
    if cnt > mx:
        ans = p
        mx = cnt

print(ans)
```

