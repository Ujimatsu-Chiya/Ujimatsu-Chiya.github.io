---
title: Project Euler 696
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 696
## 题目
### Mahjong

The game of Mahjong is played with tiles belonging to $s$ <i>suits</i>. Each tile also has a <i>number</i> in the range $1\ldots n$, and for each suit/number combination there are exactly four indistinguishable tiles with that suit and number. (The real Mahjong game also contains other bonus tiles, but those will not feature in this problem.)

A <i>winning hand</i> is a collection of $3t+2$ Tiles (where $t$ is a fixed integer) that can be arranged as $t$ <i>Triples</i> and one <i>Pair</i>, where:
<ul><li>A <i>Triple</i> is either a <i>Chow</i> or a <i>Pung</i></li>
<li>A <i>Chow</i> is three tiles of the same suit and consecutive numbers</li>
<li>A <i>Pung</i> is three identical tiles (same suit and same number)</li>
<li>A <i>Pair</i> is two identical tiles (same suit and same number)</li>
</ul>For example, here is a winning hand with $n=9$, $s=3$, $t=4$, consisting in this case of two Chows, two Pungs, and one Pair:
<div class="center">
<img src="project/images/p696_mahjong_1.png" alt="A winning Mahjong hand" /></div>

Note that sometimes the same collection of tiles can be represented as $t$ Triples and one Pair in more than one way. This only counts as one winning hand. For example, this is considered to be the same winning hand as above, because it consists of the same tiles:
<div class="center">
<img src="project/images/p696_mahjong_2.png" alt="Alternative arrangement of the same hand" /></div>

Let $w(n, s, t)$ be the number of distinct winning hands formed of $t$ Triples and one Pair, where there are $s$ suits available and tiles are numbered up to $n$.

For example, with a single suit and tiles numbered up to 4, we have $w(4, 1, 1) = 20$: there are 12 winning hands consisting of a Pung and a Pair, and another 8 containing a Chow and a Pair. You are also given that $w(9, 1, 4) = 13259$, $w(9, 3, 4) = 5237550$, and $w(1000, 1000, 5) \equiv 107662178 \pmod{1\,000\,000\,007}$.

Find $w(10^8, 10^8, 30)$. Give your answer modulo $1\,000\,000\,007$.



# Project Euler 696
## 题目
### Mahjong

The game of Mahjong is played with tiles belonging to $s$ <i>suits</i>. Each tile also has a <i>number</i> in the range $1\ldots n$, and for each suit/number combination there are exactly four indistinguishable tiles with that suit and number. (The real Mahjong game also contains other bonus tiles, but those will not feature in this problem.)
A <i>winning hand</i> is a collection of $3t+2$ Tiles (where $t$ is a fixed integer) that can be arranged as $t$ <i>Triples</i> and one <i>Pair</i>, where:
<ul>
<li>A <i>Triple</i> is either a <i>Chow</i> or a <i>Pung</i></li>
<li>A <i>Chow</i> is three tiles of the same suit and consecutive numbers</li>
<li>A <i>Pung</i> is three identical tiles (same suit and same number)</li>
<li>A <i>Pair</i> is two identical tiles (same suit and same number)</li>
</ul>
For example, here is a winning hand with $n=9$, $s=3$, $t=4$, consisting in this case of two Chows, two Pungs, and one Pair:
<img src="https://projecteuler.net/project/images/p696_mahjong_1.png" alt="A winning Mahjong hand">
Note that sometimes the same collection of tiles can be represented as $t$ Triples and one Pair in more than one way. This only counts as one winning hand. For example, this is considered to be the same winning hand as above, because it consists of the same tiles:
<img src="https://projecteuler.net/project/images/p696_mahjong_2.png" alt="Alternative arrangement of the same hand">
Let $w(n, s, t)$ be the number of distinct winning hands formed of $t$ Triples and one Pair, where there are $s$ suits available and tiles are numbered up to $n$.
For example, with a single suit and tiles numbered up to $4$, we have $w(4, 1, 1) = 20$: there are $12$ winning hands consisting of a Pung and a Pair, and another $8$ containing a Chow and a Pair. You are also given that $w(9, 1, 4) = 13259$, $w(9, 3, 4) = 5237550$, and $w(1000, 1000, 5) \equiv 107662178 \pmod{1\ 000\ 000\ 007}$.
Find $w(10^8, 10^8, 30)$. Give your answer modulo $1\ 000\ 000\ 007$.


## 解决方案


## 代码


