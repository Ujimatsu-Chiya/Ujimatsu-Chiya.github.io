---
title: Project Euler 437
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 437
## 题目
### Fibonacci primitive roots


When we calculate 8^n modulo 11 for n=0 to 9 we get: 1, 8, 9, 6, 4, 10, 3, 2, 5, 7.<br />
As we see all possible values from 1 to 10 occur. So 8 is a <b>primitive root</b> of 11.<br />
But there is more:<br />
If we take a closer look we see:<br />
1+8=9<br />
8+9=17≡6 mod 11<br />
9+6=15≡4 mod 11<br />
6+4=10<br />
4+10=14≡3 mod 11<br />
10+3=13≡2 mod 11<br />
3+2=5<br />
2+5=7<br />
5+7=12≡1 mod 11.

So the powers of 8 mod 11 are cyclic with period 10, and 8^n + 8^n+1 ≡ 8^n+2 (mod 11).<br />
8 is called a <b>Fibonacci primitive root</b> of 11.<br />
Not every prime has a Fibonacci primitive root.<br />
There are 323 primes less than 10000 with one or more Fibonacci primitive roots and the sum of these primes is 1480491.<br />
Find the sum of the primes less than 100,000,000 with at least one Fibonacci primitive root.




# Project Euler 437
## 题目
### Fibonacci primitive roots

When we calculate 8^n modulo 11 for n=0 to 9 we get: 1, 8, 9, 6, 4, 10, 3, 2, 5, 7.<br>As we see all possible values from 1 to 10 occur. So 8 is a **primitive root** of 11.<br>But there is more:<br>If we take a closer look we see:<br>1+8=9<br>8+9=17≡6 mod 11<br>9+6=15≡4 mod 11<br>6+4=10<br>4+10=14≡3 mod 11<br>10+3=13≡2 mod 11<br>3+2=5<br>2+5=7<br>5+7=12≡1 mod 11.
So the powers of 8 mod 11 are cyclic with period 10, and 8^n + 8^n+1 ≡ 8^n+2 (mod 11).<br>8 is called a **Fibonacci primitive root** of 11.<br>Not every prime has a Fibonacci primitive root.<br>There are 323 primes less than 10000 with one or more Fibonacci primitive roots and the sum of these primes is 1480491.<br>Find the sum of the primes less than 100,000,000 with at least one Fibonacci primitive root.


## 解决方案


## 代码


