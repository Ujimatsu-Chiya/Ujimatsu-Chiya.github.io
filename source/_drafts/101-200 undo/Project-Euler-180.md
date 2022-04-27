---
title: Project Euler 180
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 180
## 题目
### Rational zeros of a function of three variables

For any integer <var>n</var>, consider the three functions
<p class="margin_left"><var>f</var>_1,<var>n</var>(<var>x</var>,<var>y</var>,<var>z</var>) = <var>x</var>^<var>n</var>+1 + <var>y</var>^<var>n</var>+1 − <var>z</var>^<var>n</var>+1<br /><var>f</var>_2,<var>n</var>(<var>x</var>,<var>y</var>,<var>z</var>) = (<var>xy</var> + <var>yz</var> + <var>zx</var>)*(<var>x</var>^<var>n</var>-1 + <var>y</var>^<var>n</var>-1 − <var>z</var>^<var>n</var>-1)<br /><var>f</var>_3,<var>n</var>(<var>x</var>,<var>y</var>,<var>z</var>) = <var>xyz</var>*(<var>x</var>^<var>n</var>-2 + <var>y</var>^<var>n</var>-2 − <var>z</var>^<var>n</var>-2)
and their combination
<p class="margin_left"><var>f</var>_<var>n</var>(<var>x</var>,<var>y</var>,<var>z</var>) = <var>f</var>_1,<var>n</var>(<var>x</var>,<var>y</var>,<var>z</var>) + <var>f</var>_2,<var>n</var>(<var>x</var>,<var>y</var>,<var>z</var>) − <var>f</var>_3,<var>n</var>(<var>x</var>,<var>y</var>,<var>z</var>)
We call (<var>x</var>,<var>y</var>,<var>z</var>) a golden triple of order <var>k</var> if <var>x</var>, <var>y</var>, and <var>z</var> are all rational numbers of the form <var>a</var> / <var>b</var> with<br />
0 &lt; <var>a</var> &lt; <var>b</var> ≤ <var>k</var> and there is (at least) one integer <var>n</var>, so that <var>f</var>_<var>n</var>(<var>x</var>,<var>y</var>,<var>z</var>) = 0.
Let <var>s</var>(<var>x</var>,<var>y</var>,<var>z</var>) = <var>x</var> + <var>y</var> + <var>z</var>.<br />
Let <var>t</var> = <var>u</var> / <var>v</var> be the sum of all distinct <var>s</var>(<var>x</var>,<var>y</var>,<var>z</var>) for all golden triples (<var>x</var>,<var>y</var>,<var>z</var>) of order 35.<br /> All the <var>s</var>(<var>x</var>,<var>y</var>,<var>z</var>) and <var>t</var>  must be in reduced form.
Find <var>u</var> + <var>v</var>.


# Project Euler 180
## 题目
### Rational zeros of a function of three variables
For any integer $n$, consider the three functions
$$f_{1,n}(x,y,z)=x^{n+1}+y^{n+1}-z^{n+1}$$<br>$$f_{2,n}(x,y,z)=(xy+yz+zx)(x^{n-1}+y^{n-1}-z^{n-1})$$<br>$$f_{3,n}(x,y,z)=xyz(x^{n-2}+y^{n-2}-z^{n-2})$$
and their combination
$$f_n(x,y,z)=f_{1,n}(x,y,z)+f_{2,n}(x,y,z)-f_{3,n}(x,y,z)$$
We call $(x,y,z)$ a golden triple of order $k$ if $x$, $y$, and $z$ are all rational numbers of the form $a / b$ with $0 &lt;a &lt; b \le k$ and there is (at least) one integer $n$, so that $f_n(x,y,z) = 0$.
Let $s(x,y,z) = x + y + z$.<br>Let $t = u / v$ be the sum of all distinct $s(x,y,z)$ for all golden triples $(x,y,z)$ of order $35$.<br>All the $s(x,y,z)$ and $t$ must be in reduced form.
Find $u + v$.


## 解决方案


## 代码


