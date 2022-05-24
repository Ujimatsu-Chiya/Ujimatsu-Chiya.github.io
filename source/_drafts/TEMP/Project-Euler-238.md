---
title: Project Euler 238
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 238
## 题目
### Infinite string tour

Create a sequence of numbers using the "Blum Blum Shub" pseudo-random number generator:

<center><table class="p238"><tr><td style="text-align:right;"><var>s</var>_0</td>
    <td>=</td>
    <td>14025256</td>
  </tr><tr><td><var>s</var>_<var>n</var>+1</td>
    <td>=</td>
    <td><var>s</var>_<var>n</var>^2 mod 20300713</td>
  </tr></table></center>

Concatenate these numbers  <var>s</var>_0<var>s</var>_1<var>s</var>_2\dots to create a string <var>w</var> of infinite length.<br />
Then, <var>w</var> = <span style="font-family:'courier new';font-size:12pt;color:#3333ff;">14025256741014958470038053646\dots</span>

For a positive integer <var>k</var>, if no substring of <var>w</var> exists with a sum of digits equal to <var>k</var>, <var>p</var>(<var>k</var>) is defined to be zero. If at least one substring of <var>w</var> exists with a sum of digits equal to <var>k</var>, we define <var>p</var>(<var>k</var>) = <var>z</var>, where <var>z</var> is the starting position of the earliest such substring.

For instance:

The substrings <span style="font-family:'courier new';font-size:12pt;color:#3333ff;">1</span>, <span style="font-family:'courier new';font-size:12pt;color:#3333ff;">14</span>, <span style="font-family:'courier new';font-size:12pt;color:#3333ff;">1402</span>, \dots <br />
with respective sums of digits equal to 1, 5, 7, \dots<br />
start at position <b>1</b>, hence <var>p</var>(1) = <var>p</var>(5) = <var>p</var>(7) = \dots = <b>1</b>.

The substrings <span style="font-family:'courier new';font-size:12pt;color:#3333ff;">4</span>, <span style="font-family:'courier new';font-size:12pt;color:#3333ff;">402</span>, <span style="font-family:'courier new';font-size:12pt;color:#3333ff;">4025</span>, \dots<br />
with respective sums of digits equal to 4, 6, 11, \dots<br />
start at position <b>2</b>, hence <var>p</var>(4) = <var>p</var>(6) = <var>p</var>(11) = \dots = <b>2</b>.

The substrings <span style="font-family:'courier new';font-size:12pt;color:#3333ff;">02</span>, <span style="font-family:'courier new';font-size:12pt;color:#3333ff;">0252</span>, \dots<br />
with respective sums of digits equal to 2, 9, \dots<br />
start at position <b>3</b>, hence <var>p</var>(2) = <var>p</var>(9) = \dots = <b>3</b>.

Note that substring <span style="font-family:'courier new';font-size:12pt;color:#3333ff;">025</span> starting at position <b>3</b>, has a sum of digits equal to 7, but there was an earlier substring (starting at position <b>1</b>) with a sum of digits equal to 7, so <var>p</var>(7) = 1, <i>not</i> 3.

We can verify that, for 0 < <var>k</var> \le 10^3, <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> <var>p</var>(<var>k</var>) = 4742.

Find <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> <var>p</var>(<var>k</var>), for 0 < <var>k</var> \le 2\times10^15.


# Project Euler 238
## 题目
### Infinite string tour

Create a sequence of numbers using the “Blum Blum Shub” pseudo-random number generator:
<center>$s\_0=14025256$
$s\_{n+1}=s\_n^2 \text{ mod }20300713$
</center>

Concatenate these numbers &thinsp;s_0s_1s_2\dots to create a string w of infinite length.<br>Then, w&thinsp;=&thinsp;<span style="font-family:courier new;font-size:12pt;color:#0000ff;">14025256741014958470038053646\dots</span>
For a positive integer k, if no substring of w exists with a sum of digits equal to k, p(k) is defined to be zero. If at least one substring of w exists with a sum of digits equal to k, we define p(k)&thinsp;=&thinsp;z, where z is the starting position of the earliest such substring.
For instance:
The substrings <span style="font-family:courier new;font-size:12pt;color:#0000ff;">1</span>, <span style="font-family:courier new;font-size:12pt;color:#0000ff;">14</span>, <span style="font-family:courier new;font-size:12pt;color:#0000ff;">1402</span>, \dots<br>with respective sums of digits equal to 1, 5, 7, \dots<br>start at position <b>1</b>, hence p(1)&thinsp;=&thinsp;p(5)&thinsp;=&thinsp;p(7)&thinsp;=&thinsp;\dots&thinsp;=&thinsp;<b>1</b>.
The substrings <span style="font-family:courier new;font-size:12pt;color:#0000ff;">4</span>, <span style="font-family:courier new;font-size:12pt;color:#0000ff;">402</span>, <span style="font-family:courier new;font-size:12pt;color:#0000ff;">4025</span>, \dots<br>with respective sums of digits equal to 4, 6, 11, \dots<br>start at position <b>2</b>, hence p(4)&thinsp;=&thinsp;p(6)&thinsp;=&thinsp;p(11)&thinsp;=&thinsp;\dots&thinsp;=&thinsp;<b>2</b>.
The substrings <span style="font-family:courier new;font-size:12pt;color:#0000ff;">02</span>, <span style="font-family:courier new;font-size:12pt;color:#0000ff;">0252</span>, \dots<br>with respective sums of digits equal to 2, 9, \dots<br>start at position <b>3</b>, hence p(2)&thinsp;=&thinsp;p(9)&thinsp;=&thinsp;\dots&thinsp;=&thinsp;<b>3</b>.
Note that substring <span style="font-family:courier new;font-size:12pt;color:#0000ff;">025</span> starting at position <b>3</b>, has a sum of digits equal to 7, but there was an earlier substring (starting at position <b>1</b>) with a sum of digits equal to 7, so p(7)&thinsp;=&thinsp;1, <i>not</i> 3.
We can verify that, for 0&thinsp;<&thinsp;k&thinsp;\le&thinsp;10^3, \sum&thinsp;p(k) = 4742.
Find \sum&thinsp;p(k), for 0&thinsp;<&thinsp;k&thinsp;\le&thinsp;2·10^15.


## 解决方案


## 代码


