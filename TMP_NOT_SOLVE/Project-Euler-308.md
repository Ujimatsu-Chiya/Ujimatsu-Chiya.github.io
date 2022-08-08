---
title: Project Euler 308
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 308
## 题目
### An amazing Prime-generating Automaton


A program written in the programming language Fractran consists of a list of fractions.

The internal state of the Fractran Virtual Machine is a positive integer, which is initially set to a seed value. Each iteration of a Fractran program multiplies the state integer by the first fraction in the list which will leave it an integer.

For example, one of the Fractran programs that John Horton Conway wrote for prime-generation consists of the following 14 fractions:

$$\dfrac{17}{91}, \dfrac{78}{85}, \dfrac{19}{51}, \dfrac{23}{38}, \dfrac{29}{33}, \dfrac{77}{29}, \dfrac{95}{23}, \dfrac{77}{19}, \dfrac{1}{17}, \dfrac{11}{13}, \dfrac{13}{11}, \dfrac{15}{2}, \dfrac{1}{7}, \dfrac{55}{1}$$

Starting with the seed integer 2, successive iterations of the program produce the sequence:<br />
15, 825, 725, 1925, 2275, 425, \dots, 68, <b>4</b>, 30, \dots, 136, <b>8</b>, 60, \dots, 544, <b>32</b>, 240, \dots

The powers of 2 that appear in this sequence are 2^2, 2^3, 2^5, \dots<br />
It can be shown that <i>all</i> the powers of 2 in this sequence have prime exponents and that <i>all</i> the primes appear as exponents of powers of 2, in proper order!

If someone uses the above Fractran program to solve Project Euler Problem 7 (find the 10001^st prime), how many iterations would be needed until the program produces 2^10001st prime ?


# Project Euler 308
## 题目
### An amazing Prime-generating Automaton

A program written in the programming language Fractran consists of a list of fractions.
The internal state of the Fractran Virtual Machine is a positive integer, which is initially set to a seed value. Each iteration of a Fractran program multiplies the state integer by the first fraction in the list which will leave it an integer.
For example, one of the Fractran programs that John Horton Conway wrote for prime-generation consists of the following 14 fractions:
$\frac{17}{91}$, $\frac{78}{85}$, $\frac{19}{51}$, $\frac{23}{38}$, $\frac{29}{33}$, $\frac{77}{29}$, $\frac{95}{23}$, $\frac{77}{19}$, $\frac{1}{17}$, $\frac{11}{13}$, $\frac{13}{11}$, $\frac{15}{2}$, $\frac{1}{7}$, $\frac{55}{1}$. 
Starting with the seed integer 2, successive iterations of the program produce the sequence:<br>15, 825, 725, 1925, 2275, 425, \dots, 68, **4**, 30, \dots, 136, **8**, 60, \dots, 544, **32**, 240, \dots
The powers of 2 that appear in this sequence are 2^2, 2^3, 2^5, \dots<br>It can be shown that <i>all</i> the powers of 2 in this sequence have prime exponents and that <i>all</i> the primes appear as exponents of powers of 2, in proper order!
If someone uses the above Fractran program to solve Project Euler Problem 7 (find the 10001^st prime), how many iterations would be needed until the program produces 2^10001st prime?


## 解决方案


## 代码


