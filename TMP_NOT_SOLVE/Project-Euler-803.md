---
title: Project Euler 803
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 803
## 题目
### Pseudorandom sequence


<b>Rand48</b> is a pseudorandom number generator used by some programming languages. It generates a sequence from any given integer $a_0$ using the rule $a_n = (25214903917 \cdot a_{n - 1} + 11) \bmod 2^{48}$.


Let $b_n = \lfloor a_n / 2^{16} \rfloor \bmod 52$.
The sequence $b_0, b_1, \dots$ is translated to an infinite string $c = c_0c_1\dots$ via the rule:<br />
$0 \rightarrow$ a, $1\rightarrow$ b, $\dots$, $25 \rightarrow$ z, $26 \rightarrow$ A, $27 \rightarrow$ B, $\dots$, $51 \rightarrow$ Z.


For example, if we choose $a_0 = 123456$, then the string $c$ starts with: "bQYicNGCY$\dots$".<br />
Moreover, starting from index $100$, we encounter the substring "RxqLBfWzv" for the first time.


Alternatively, if $c$ starts with "EULERcats$\dots$", then $a_0$ must be $78580612777175$.


Now suppose that the string $c$ starts with "PuzzleOne$\dots$".<br />
Find the starting index of the first occurrence of the substring "LuckyText" in $c$.





## 解决方案


## 代码


