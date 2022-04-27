---
title: Project Euler 122
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 122
## 题目
### Efficient exponentiation

The most naive way of computing <i>n</i>^15 requires fourteen multiplications:
<p style="margin-left:100px;"><i>n</i> × <i>n</i> × \dots × <i>n</i> = <i>n</i>^15
But using a "binary" method you can compute it in six multiplications:
<p style="margin-left:100px;"><i>n</i> × <i>n</i> = <i>n</i>^2<br /><i>n</i>^2 × <i>n</i>^2 = <i>n</i>^4<br /><i>n</i>^4 × <i>n</i>^4 = <i>n</i>^8<br /><i>n</i>^8 × <i>n</i>^4 = <i>n</i>^12<br /><i>n</i>^12 × <i>n</i>^2 = <i>n</i>^14<br /><i>n</i>^14 × <i>n</i> = <i>n</i>^15
However it is yet possible to compute it in only five multiplications:
<p style="margin-left:100px;"><i>n</i> × <i>n</i> = <i>n</i>^2<br /><i>n</i>^2 × <i>n</i> = <i>n</i>^3<br /><i>n</i>^3 × <i>n</i>^3 = <i>n</i>^6<br /><i>n</i>^6 × <i>n</i>^6 = <i>n</i>^12<br /><i>n</i>^12 × <i>n</i>^3 = <i>n</i>^15
We shall define m(<i>k</i>) to be the minimum number of multiplications to compute <i>n</i>^<i>k</i>; for example m(15) = 5.
For 1 ≤ <i>k</i> ≤ 200, find <span style="font-family:'times new roman';font-size:13pt;">∑</span> m(<i>k</i>).



# Project Euler 122
## 题目
### Efficient exponentiation
The most naive way of computing n^15 requires fourteen multiplications:
n × n × \dots × n = n^15
But using a “binary” method you can compute it in six multiplications:
n × n = n^2<br>n^2 × n^2 = n^4<br>n^4 × n^4 = n^8<br>n^8 × n^4 = n^12<br>n^12 × n^2 = n^14<br>n^14 × n = n^15
However it is yet possible to compute it in only five multiplications:
n × n = n^2<br>n^2 × n = n^3<br>n^3 × n^3 = n^6<br>n^6 × n^6 = n^12<br>n^12 × n^3 = n^15
We shall define m(k) to be the minimum number of multiplications to compute n^k; for example m(15) = 5.
For 1 ≤ k ≤ 200, find ∑m(k).


## 解决方案


## 代码


