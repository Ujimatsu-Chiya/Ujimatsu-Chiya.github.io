---
title: Project Euler 230
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    




# Project Euler 230
## 题目
### Fibonacci Words

For any two strings of digits, $A$ and $B$, we define $F_{A,B}$ to be the sequence $(A,B,AB,BAB,ABBAB,\dots)$ in which each term is the concatenation of the previous two.

Further, we define $D_{A,B}(n)$ to be the $n^{\text{th}}$ digit in the first term of $F_{A,B}$ that contains at least $n$ digits.
Example:

Let $A=1415926535, B=8979323846$. We wish to find $D_{A,B}(35)$, say.

The first few terms of $F_{A,B}$ are:

$1415926535$<br>
$8979323846$<br>
$14159265358979323846$<br>
$897932384614159265358979323846$<br>
$1415926535897932384689793238461415\color{red}{9}$ $265358979323846$

Then $D_{A,B}(35)$ is the $35^{\text{th}}$ digit in the fifth term, which is $9$.

Now we use for $A$ the first $100$ digits of $\pi$ behind the decimal point:

1415926535897932384626433832795028841971693993751058209749445923078164062862089986280348253421170679 

and for B the next hundred digits:

8214808651328230664709384460955058223172535940812848111745028410270193852110555964462294895493038196 .

Find $\sum_{n = 0,1,\dots,17}  10^n\times D_{A,B}((127+19n)\times7^n)$.


## 解决方案

这题不需要真正地计算出这些字符串数组$F_{A,B}$的具体内容，只需要通过递推式计算出$F_{A,B}$中每个字符串的长度。

假设$F_{A,B}[i][j]$为序列$F_{A,B}$的第$i$个字符串的第$j$个字符。由于$F_{A,B}[i]$是由$F_{A,B}[i-2]$和$F_{A,B}[i-1]$拼接而成。因此只需通过长度判断，就可以通过下标定位到前面两个字符串。如果需要查询的下标$k$落在$F_{A,B}[i-2]$中，那么转而在字符串$F_{A,B}[i-2]$继续查找，否则在$F_{A,B}[i-1]$中继续查找。如此迭代，直到回到初始字符串$A,B$，即可得到答案。


## 代码


```py
N = 17
A = "1415926535897932384626433832795028841971693993751058209749445923078164062862089986280348253421170679"
B = "8214808651328230664709384460955058223172535940812848111745028410270193852110555964462294895493038196"

M = 100
len_F = [len(A), len(B)]
for i in range(M):
    len_F.append(len_F[-2] + len_F[-1])


def get_digit(f: int, pos: int):
    if f == 0:
        return A[pos - 1]
    elif f == 1:
        return B[pos - 1]
    else:
        if pos <= len_F[f - 2]:
            return get_digit(f - 2, pos)
        else:
            return get_digit(f - 1, pos - len_F[f - 2])


ans = 0
for n in range(N + 1):
    p = (127 + 19 * n) * (7 ** n)
    for i in range(M):
        if len_F[i] >= p:
            ans += int(get_digit(i, p)) * 10 ** n
            break
print(ans)

```