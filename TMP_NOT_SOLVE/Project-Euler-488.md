---
title: Project Euler 488
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 488
## 题目
### Unbalanced Nim

Alice and Bob have enjoyed playing <b>Nim</b> every day. However, they finally got bored of playing ordinary three-heap Nim.<br />
So, they added an extra rule:

- Must not make two heaps of the same size.

The triple (<var>a</var>,<var>b</var>,<var>c</var>) indicates the size of three heaps.<br />
Under this extra rule, (2,4,5) is one of the losing positions for the next player.

To illustrate:<br />
- Alice moves to (2,4,3)<br />
- Bob   moves to (0,4,3)<br />
- Alice moves to (0,2,3)<br />
- Bob   moves to (0,2,1)

Unlike ordinary three-heap Nim, (0,1,2) and its permutations are the end states of this game.

For an integer <var>N</var>, we define F(<var>N</var>) as the sum of <var>a</var>+<var>b</var>+<var>c</var> for all the losing positions for the next player, with 0 < <var>a</var> < <var>b</var> < <var>c</var> < <var>N</var>.

For example, F(8) = 42, because there are 4 losing positions for the next player, (1,3,5), (1,4,6), (2,3,6) and (2,4,5).<br />
We can also verify that F(128) = 496062.

Find the last 9 digits of F(10^18).


# Project Euler 488
## 题目
### Unbalanced Nim

Alice and Bob have enjoyed playing **Nim** every day. However, they finally got bored of playing ordinary three-heap Nim.<br>So, they added an extra rule:
<ul>
<li>Must not make two heaps of the same size.</li>
</ul>
The triple (a,b,c) indicates the size of three heaps.<br>Under this extra rule, (2,4,5) is one of the losing positions for the next player.
To illustrate:
<ul>
<li>Alice moves to (2,4,3)</li>
<li>Bob   moves to (0,4,3)</li>
<li>Alice moves to (0,2,3)</li>
<li>Bob   moves to (0,2,1)</li>
</ul>
Unlike ordinary three-heap Nim, (0,1,2) and its permutations are the end states of this game.
For an integer N, we define F(N) as the sum of a+b+c for all the losing positions for the next player, with 0 < a < b < c < N.
For example, F(8) = 42, because there are 4 losing positions for the next player, (1,3,5), (1,4,6), (2,3,6) and (2,4,5).<br>We can also verify that F(128) = 496062.
Find the last 9 digits of F(10^18).


## 解决方案


## 代码


