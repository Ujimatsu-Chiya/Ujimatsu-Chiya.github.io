---
title: Project Euler 666
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 666
## 题目
### Polymorphic Bacteria


Members of a species of bacteria occur in two different types: $\alpha$ and $\beta$. Individual bacteria are capable of multiplying and mutating between the types according to the following rules:
<ul><li>Every minute, each individual will simultaneously undergo some kind of transformation.</li>
<li>Each individual $A$ of type $\alpha$ will, independently, do one of the following (at random with equal probability):
<ul><li>clone itself, resulting in a new bacterium of type $\alpha$ (alongside $A$ who remains)</li>
<li>split into 3 new bacteria of type $\beta$ (replacing $A$)</li>
</ul></li>

<li>Each individual $B$ of type $\beta$ will, independently, do one of the following (at random with equal probability):
<ul><li>spawn a new bacterium of type $\alpha$ (alongside $B$ who remains)</li>
<li>die</li>
</ul></li></ul>
If a population starts with a single bacterium of type $\alpha$, then it can be shown that there is a 0.07243802 probability that the population will eventually die out, and a 0.92756198 probability that the population will last forever. These probabilities are given rounded to 8 decimal places.


Now consider another species of bacteria, $S_{k,m}$ (where $k$ and $m$ are positive integers), which occurs in $k$ different types $\alpha_i$ for $0\le i< k$. The rules governing this species' lifecycle involve the sequence $r_n$ defined by:

<ul style="list-style-type:none;"><li>$r_0 = 306$</li>
<li>$r_{n+1} = r_n^2 \bmod 10\,007$</li>
</ul>
Every minute, for each $i$, each bacterium $A$ of type $\alpha_i$ will independently choose an integer $j$ uniformly at random in the range $0\le j<m$. What it then does depends on $q = r_{im+j} \bmod 5$:
<ul><li>If $q=0$, $A$ dies.</li>
<li>If $q=1$, $A$ clones itself, resulting in a new bacterium of type $\alpha_i$ (alongside $A$ who remains).</li>
<li>If $q=2$, $A$ mutates, changing into type $\alpha_{(2i) \bmod k}$.</li>
<li>If $q=3$, $A$ splits into 3 new bacteria of type $\alpha_{(i^2+1) \bmod k}$ (replacing $A$).</li>
<li>If $q=4$, $A$ spawns a new bacterium of type $\alpha_{(i+1) \bmod k}$ (alongside $A$ who remains).</li>
</ul>
In fact, our original species was none other than $S_{2,2}$, with $\alpha=\alpha_0$ and $\beta=\alpha_1$.


Let $P_{k,m}$ be the probability that a population of species $S_{k,m}$, starting with a single bacterium of type $\alpha_0$, will eventually die out. So $P_{2,2} = 0.07243802$. You are also given that $P_{4,3} = 0.18554021$ and $P_{10,5} = 0.53466253$, all rounded to 8 decimal places.


Find $P_{500,10}$, and give your answer rounded to 8 decimal places.



# Project Euler 666
## 题目
### Polymorphic Bacteria

Members of a species of bacteria occur in two different types: $\alpha$ and $\beta$. Individual bacteria are capable of multiplying and mutating between the types according to the following rules:
<ul>
<li>Every minute, each individual will simultaneously undergo some kind of transformation.</li>
<li>Each individual $A$ of type $\alpha$ will, independently, do one of the following (at random with equal probability):<ul>
<li>clone itself, resulting in a new bacterium of type $\alpha$ (alongside $A$ who remains)</li>
<li>split into $3$ new bacteria of type $\beta$ (replacing $A$)</li>
</ul>
</li>
<li>Each individual $B$ of type $\beta$ will, independently, do one of the following (at random with equal probability):<ul>
<li>spawn a new bacterium of type $\alpha$ (alongside $B$ who remains)    </li>
<li>die</li>
</ul>
</li>
</ul>
If a population starts with a single bacterium of type $\alpha$, then it can be shown that there is a $0.07243802$ probability that the population will eventually die out, and a $0.92756198$ probability that the population will last forever. These probabilities are given rounded to $8$ decimal places.
Now consider another species of bacteria, $S_{k,m}$ (where $k$ and $m$ are positive integers), which occurs in $k$ different types $\alpha_i$ for $0\le i< k$. The rules governing this species’ lifecycle involve the sequence $r_n$ defined by:<br>    $r_0 = 306$<br>    $r_{n+1} = r_n^2 \bmod 10\ 007$
Every minute, for each $i$, each bacterium $A$ of type $\alpha_i$ will independently choose an integer $j$ uniformly at random in the range $0\le j<m$. What it then does depends on $q = r_{im+j} \bmod 5$:
<ul>
<li>If $q=0$, $A$ dies.</li>
<li>If $q=1$, $A$ clones itself, resulting in a new bacterium of type $\alpha_i$ (alongside $A$ who remains).</li>
<li>If $q=2$, $A$ mutates, changing into type $\alpha_{(2i) \bmod k}$.</li>
<li>If $q=3$, $A$ splits into 3 new bacteria of type $\alpha_{(i^2+1) \bmod k}$ (replacing $A$).</li>
<li>If $q=4$, $A$ spawns a new bacterium of type $\alpha_{(i+1) \bmod k}$ (alongside $A$ who remains).</li>
</ul>
In fact, our original species was none other than $S_{2,2}$, with $\alpha=\alpha_0$ and $\beta=\alpha_1$.
Let $P_{k,m}$ be the probability that a population of species $S_{k,m}$, starting with a single bacterium of type $\alpha_0$, will eventually die out. So $P_{2,2} = 0.07243802$. You are also given that $P_{4,3} = 0.18554021$ and $P_{10,5} = 0.53466253$, all rounded to $8$ decimal places.
Find $P_{500,10}$, and give your answer rounded to $8$ decimal places.


## 解决方案


## 代码


