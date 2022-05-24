---
title: Project Euler 534
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 534
## 题目
### Weak Queens

The classical <b>eight queens puzzle</b> is the well known problem of placing eight chess queens on a 8\times8 chessboard so that no two queens threaten each other. Allowing configurations to reappear in rotated or mirrored form, a total of 92 distinct configurations can be found for eight queens. The general case asks for the number of distinct ways of placing <var>n</var> queens on a <var>n</var>\times<var>n</var> board, e.g. you can find 2 distinct configurations for <var>n</var>=4.

Let's define a <i>weak queen</i> on a <var>n</var>\times<var>n</var> board to be a piece which can move any number of squares if moved horizontally, but a maximum of <var>n</var>−1−<var>w</var> squares if moved vertically or diagonally, 0\lew<n being the "weakness factor". For example, a weak queen on a <var>n</var>\times<var>n</var> board with a weakness factor of <var>w</var>=1 located in the bottom row will not be able to threaten any square in the top row as the weak queen would need to move <var>n</var>−1 squares vertically or diagonally to get there, but may only move <var>n</var>−2 squares in these directions. In contrast, the weak queen is not handicapped horizontally, thus threatening every square in its own row, independently from its current position in that row.

Let Q(<var>n</var>,<var>w</var>) be the number of ways <var>n</var> weak queens with weakness factor <var>w</var> can be placed on a <var>n</var>\times<var>n</var> board so that no two queens threaten each other. It can be shown, for example, that Q(4,0)=2, Q(4,2)=16 and Q(4,3)=256.

Let $S(n)=\displaystyle\sum_{w=0}^{n-1} Q(n,w)$.

You are given that S(4)=276 and S(5)=3347.

Find S(14).


# Project Euler 534
## 题目
### Weak Queens

The classical <b>eight queens puzzle</b> is the well known problem of placing eight chess queens on a 8\times8 chessboard so that no two queens threaten each other. Allowing configurations to reappear in rotated or mirrored form, a total of 92 distinct configurations can be found for eight queens. The general case asks for the number of distinct ways of placing n queens on a n\timesn board, e.g. you can find 2 distinct configurations for n=4.
Lets define a <i>weak queen</i> on a n\timesn board to be a piece which can move any number of squares if moved horizontally, but a maximum of n−1−w squares if moved vertically or diagonally, 0\lew<n being the “weakness factor”. For example, a weak queen on a n\timesn board with a weakness factor of w=1 located in the bottom row will not be able to threaten any square in the top row as the weak queen would need to move n−1 squares vertically or diagonally to get there, but may only move n−2 squares in these directions. In contrast, the weak queen is not handicapped horizontally, thus threatening every square in its own row, independently from its current position in that row.
Let Q(n,w) be the number of ways n weak queens with weakness factor w can be placed on a n\timesn board so that no two queens threaten each other. It can be shown, for example, that Q(4,0)=2, Q(4,2)=16 and Q(4,3)=256.
Let $S(n)=\displaystyle\sum_{w=0}^{n-1} Q(n,w)$.
You are given that S(4)=276 and S(5)=3347.
Find S(14).


## 解决方案


## 代码


