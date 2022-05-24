---
title: Project Euler 490
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 490
## 题目
### Jumping frog

There are <var>n</var> stones in a pond, numbered 1 to <var>n</var>. Consecutive stones are spaced one unit apart.

A frog sits on stone 1. He wishes to visit each stone exactly once, stopping on stone <var>n</var>. However, he can only jump from one stone to another if they are at most 3 units apart. In other words, from stone <var>i</var>, he can reach a stone <var>j</var> if 1 \le <var>j</var> \le <var>n</var> and <var>j</var> is in the set {<var>i</var>-3, <var>i</var>-2, <var>i</var>-1, <var>i</var>+1, <var>i</var>+2, <var>i</var>+3}.

Let f(<var>n</var>) be the number of ways he can do this. For example, f(6) = 14, as shown below:<br />
1 → 2 → 3 → 4 → 5 → 6 <br />
1 → 2 → 3 → 5 → 4 → 6 <br />
1 → 2 → 4 → 3 → 5 → 6 <br />
1 → 2 → 4 → 5 → 3 → 6 <br />
1 → 2 → 5 → 3 → 4 → 6 <br />
1 → 2 → 5 → 4 → 3 → 6 <br />
1 → 3 → 2 → 4 → 5 → 6 <br />
1 → 3 → 2 → 5 → 4 → 6 <br />
1 → 3 → 4 → 2 → 5 → 6 <br />
1 → 3 → 5 → 2 → 4 → 6 <br />
1 → 4 → 2 → 3 → 5 → 6 <br />
1 → 4 → 2 → 5 → 3 → 6 <br />
1 → 4 → 3 → 2 → 5 → 6 <br />
1 → 4 → 5 → 2 → 3 → 6

Other examples are f(10) = 254 and f(40) = 1439682432976.

Let S(<var>L</var>) = \sum f(<var>n</var>)^3 for 1 \le <var>n</var> \le <var>L</var>.<br />
Examples:<br />
S(10) = 18230635<br />
S(20) = 104207881192114219<br />
S(1 000) mod 10^9 = 225031475<br />
S(1 000 000) mod 10^9 = 363486179

Find S(10^14) mod 10^9.



# Project Euler 490
## 题目
### Jumping frog

There are n stones in a pond, numbered 1 to n. Consecutive stones are spaced one unit apart.
A frog sits on stone 1. He wishes to visit each stone exactly once, stopping on stone n. However, he can only jump from one stone to another if they are at most 3 units apart. In other words, from stone i, he can reach a stone j if 1 \le j \le n and j is in the set {i-3, i-2, i-1, i+1, i+2, i+3}.
Let f(n) be the number of ways he can do this. For example, f(6) = 14, as shown below:<br>1 → 2 → 3 → 4 → 5 → 6<br>1 → 2 → 3 → 5 → 4 → 6<br>1 → 2 → 4 → 3 → 5 → 6<br>1 → 2 → 4 → 5 → 3 → 6<br>1 → 2 → 5 → 3 → 4 → 6<br>1 → 2 → 5 → 4 → 3 → 6<br>1 → 3 → 2 → 4 → 5 → 6<br>1 → 3 → 2 → 5 → 4 → 6<br>1 → 3 → 4 → 2 → 5 → 6<br>1 → 3 → 5 → 2 → 4 → 6<br>1 → 4 → 2 → 3 → 5 → 6<br>1 → 4 → 2 → 5 → 3 → 6<br>1 → 4 → 3 → 2 → 5 → 6<br>1 → 4 → 5 → 2 → 3 → 6
Other examples are f(10) = 254 and f(40) = 1439682432976.
Let S(L) = \sum f(n)^3 for 1 \le n \le L.<br>Examples:<br>S(10) = 18230635<br>S(20) = 104207881192114219<br>S(1 000) mod 10^9 = 225031475<br>S(1 000 000) mod 10^9 = 363486179
Find S(10^14) mod 10^9.


## 解决方案


## 代码


