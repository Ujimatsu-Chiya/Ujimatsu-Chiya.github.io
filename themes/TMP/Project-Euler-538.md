---
title: Project Euler 538
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 538
## 题目
### Maximum quadrilaterals

Consider a positive integer sequence <var>S</var> = (<var>s</var>_1, <var>s</var>_2, \dots, <var>s_n</var>).

Let f(<var>S</var>) be the perimeter of the maximum-area quadrilateral whose side lengths are 4 elements (<var>s_i</var>, <var>s_j</var>, <var>s_k</var>, <var>s_l</var>) of <var>S</var> (all <var>i</var>, <var>j</var>, <var>k</var>, <var>l</var> distinct). If there are many quadrilaterals with the same maximum area, then choose the one with the largest perimeter.

For example, if <var>S</var> = (8, 9, 14, 9, 27), then we can take the elements (9, 14, 9, 27) and form an <dfn title="An isosceles trapezium (US: trapezoid) is a quadrilateral where one pair of opposite sides are parallel and of different lengths, and the other pair has the same length."><b>isosceles trapezium</b></dfn> with parallel side lengths 14 and 27 and both leg lengths 9. The area of this quadrilateral is 127.611470879\dots It can be shown that this is the largest area for any quadrilateral that can be formed using side lengths from <var>S</var>. Therefore, f(<var>S</var>) = 9 + 14 + 9 + 27 = 59.

Let <var>u_n</var> = 2^B(3<var>n</var>) + 3^B(2<var>n</var>) + B(<var>n</var>+1), where B(<var>k</var>) is the number of 1 bits of <var>k</var> in base 2.<br />
For example, B(6) = 2, B(10) = 2 and B(15) = 4, and <var>u</var>_5 = 2^4 + 3^2 + 2 = 27.

Also, let <var>U_n</var> be the sequence (<var>u</var>_1, <var>u</var>_2, \dots, <var>u_n</var>).<br />
For example, <var>U</var>_10 = (8, 9, 14, 9, 27, 16, 36, 9, 27, 28).

It can be shown that f(<var>U</var>_5) = 59, f(<var>U</var>_10) = 118, f(<var>U</var>_150) = 3223.<br />
It can also be shown that <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> f(<var>U_n</var>) = 234761 for 4 \le n \le 150.<br />
Find <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> f(<var>U_n</var>) for 4 \le n \le 3 000 000.


# Project Euler 538
## 题目
### Maximum quadrilaterals

Consider a positive integer sequence S=(s_1,s_2,\dots,s_n).
Let f(S) be the perimeter of the maximum-area quadrilateral whose side lengths are 4 elements (s_i, s_j, s_k, s_l) of S (all i, j, k, l distinct). If there are many quadrilaterals with the same maximum area, then choose the one with the largest perimeter.
For example, if S=(8,9,14,9,27), then we can take the elements (9,14,9,27) and form an <dfn title="An isosceles trapezium (US: trapezoid) is a quadrilateral where one pair of opposite sides are parallel and of different lengths, and the other pair has the same length."><b>isosceles trapezium</b></dfn> with parallel side lengths 14 and 27 and both leg lengths 9. The area of this quadrilateral is 127.611470879\dots It can be shown that this is the largest area for any quadrilateral that can be formed using side lengths from S. Therefore, f(S)=9+14+9+27=59.
Let u_n=2^B(3n)+3^B(2n)+B(n+1), where B(k) is the number of 1 bits of k in base 2.<br>For example, B(6)=2, B(10)=2 and B(15)=4, and u_5=2^4+3^2+2=27.
Also, let U_n be the sequence (u_1,u_2,\dots,u_n).<br>For example, U_10=(8,9,14,9,27,16,36,9,27,28).
It can be shown that f(U_5)=59, f(U_10)=118, f(U_150)=3223.<br>It can also be shown that \sumf(U_n)=234761 for 4\len\le150.<br>Find \sumf(U_n) for 4\len\le3000000.


## 解决方案


## 代码


