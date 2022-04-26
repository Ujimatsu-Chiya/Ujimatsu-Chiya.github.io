---
title: Project Euler 74
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 74
## 题目
### Digit factorial chains
The number $145$ is well known for the property that the sum of the factorial of its digits is equal to $145$:
$$1! + 4! + 5! = 1 + 24 + 120 = 145$$
Perhaps less well known is $169$, in that it produces the longest chain of numbers that link back to $169$; it turns out that there are only three such loops that exist:
$$\begin{aligned}
& 169 \rightarrow 363601 \rightarrow 1454 \rightarrow 169 \\ 
& 871 \rightarrow 45361 \rightarrow 871\\
& 872 \rightarrow 45362 \rightarrow 872
\end{aligned}$$

It is not difficult to prove that EVERY starting number will eventually get stuck in a loop. For example,

$$\begin{aligned}
& 69 \rightarrow 363600 \rightarrow 1454 \rightarrow 169 \rightarrow 363601 (\rightarrow 1454)\\
& 78 \rightarrow 45360 \rightarrow 871 \rightarrow 45361 (\rightarrow 871)\\
& 540 \rightarrow 145 (\rightarrow 145)
  \end{aligned}$$

Starting with $69$ produces a chain of five non-repeating terms, but the longest non-repeating chain with a starting number below one million is sixty terms.

How many chains, with a starting number below one million, contain exactly sixty non-repeating terms?

