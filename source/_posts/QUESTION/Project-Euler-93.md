---
title: Project Euler 93
tags:
  - Project Euler
mathjax: true
date: 2022-05-02 16:37:16
---

<escape><!-- more --></escape>

# Project Euler 93

## 题目

### Arithmetic expressions

By using each of the digits from the set, $\{1, 2, 3, 4\}$, exactly once, and making use of the four arithmetic operations $(+, −, *, /)$ and brackets/parentheses, it is possible to form different positive integer targets.
For example,

$8 = (4 *(1 + 3)) / 2$
$14 = 4* (3 + 1 / 2)$
$19 = 4 *(2 + 3) − 1$
$36 = 3* 4 * (2 + 1)$

Note that concatenations of the digits, like $12 + 34$, are not allowed.
Using the set, $\{1, 2, 3, 4\}$, it is possible to obtain thirty-one different target numbers of which $36$ is the maximum, and each of the numbers $1$ to $28$ can be obtained before encountering the first non-expressible number.
Find the set of four distinct digits, $a < b < c < d$, for which the longest set of consecutive positive integers, $1$ to $n$, can be obtained, giving your answer as a string: $abcd$.

## 解决方案

直接枚举。
为了加速，先将其转为后缀表达式。可以发现，转化成后缀表达式后，一共有$5$种不同的运算顺序。
将每个后缀表达式模板中，填入枚举的数字和运算符后，用后缀表达式直接做运算。

枚举量：一共有$C_9^4$个候选答案。对于每个组合，其中可以以任意顺序填入后缀表达式中，一共有$4!$种。一共要做$3$次运算，因此运算符的组合有$4^3$种。因此需要进行$C_9^4\times 4!\times 4^3\times 5=967680$次的枚举。

## 代码

```py
from itertools import permutations, product, combinations, count

# value_pos_list = [p for p in set(permutations([-1, -1, -1, 1, 1, 1, 1])) if all(sum(p[:i + 1]) > 0 for i in range(
# len(p)))]
# print(value_pos_list)
op_list = list("".join(l) for l in product("+-*/", repeat=3))


def cal(s: str):
    ls = []
    for t in s:
        if t.isdigit():
            ls.append(int(t))
        else:
            x, y = ls[-2], ls[-1]
            ls.pop()
            if t == '+':
                ls[-1] = x + y
            elif t == '-':
                ls[-1] = x - y
            elif t == '*':
                ls[-1] = x * y
            elif y:
                ls[-1] = x / y
            else:
                return 0
    w = ls[0]
    return round(w) if abs(w - round(w)) < 1e-8 else 0


def solve(values):
    st = set()
    for per in permutations(values):
        digit = "".join(str(x) for x in per)
        for op in op_list:
            st.add(cal(digit[:2] + op[0] + digit[2:] + op[1:]))
            st.add(cal(digit[:3] + op[:2] + digit[3] + op[2]))
            st.add(cal(digit[:3] + op[0] + digit[3] + op[1:]))
            st.add(cal(digit + op))
            st.add(cal(digit[:2] + op[0] + digit[2] + op[1] + digit[3] + op[2]))

    for i in count(1, 1):
        if i not in st:
            return i - 1
    return -1


mx = 0
for v in combinations(list(range(1, 10)), 4):
    w = solve(v)
    if w > mx:
        mx = w
        ans = "".join(str(x) for x in v)
print(ans)

```
