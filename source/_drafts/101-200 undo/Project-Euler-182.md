---
title: Project Euler 182
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 182
## 题目
### RSA encryption

The RSA encryption is based on the following procedure:
Generate two distinct primes <var>p</var> and <var>q</var>.<br />Compute <var>n=pq</var> and φ=(<var>p</var>-1)(<var>q</var>-1).<br />
Find an integer <var>e</var>, 1&lt;<var>e</var>&lt;φ, such that gcd(<var>e</var>,φ)=1.
A message in this system is a number in the interval [0,<var>n</var>-1].<br />
A text to be encrypted is then somehow converted to messages (numbers in the interval [0,<var>n</var>-1]).<br />
To encrypt the text,  for each message, <var>m</var>, <var>c</var>=<var>m</var>^<var>e</var> mod <var>n</var> is calculated.
To decrypt the text, the following procedure is needed: calculate <var>d</var> such that <var>ed</var>=1 mod φ, then for each encrypted message, <var>c</var>, calculate <var>m=c^d</var> mod <var>n</var>.
There exist values of <var>e</var> and <var>m</var>  such that <var>m^e</var> mod <var>n=m</var>.<br />We call messages <var>m</var> for which <var>m^e</var> mod <var>n=m</var> unconcealed messages.
An issue when choosing <var>e</var> is that there should not be too many unconcealed messages.  <br />For instance, let <var>p</var>=19 and <var>q</var>=37.<br />
Then <var>n</var>=19*37=703 and φ=18*36=648.<br />
If we choose <var>e</var>=181, then, although gcd(181,648)=1 it turns out that all possible messages<br /><var>m</var> (0≤<var>m</var>≤<var>n</var>-1) are unconcealed when calculating <var>m^e</var> mod <var>n</var>.<br />
For any valid choice of <var>e</var> there exist some unconcealed messages.<br />
It's important that the number of unconcealed messages is at a minimum.
Choose <var>p</var>=1009 and <var>q</var>=3643.<br />
Find the sum of all values of <var>e</var>, 1&lt;<var>e</var>&lt;φ(1009,3643) and gcd(<var>e</var>,φ)=1, so that the number of unconcealed messages for this value of <var>e</var> is at a minimum.


# Project Euler 182
## 题目
### RSA encryption
The RSA encryption is based on the following procedure:
Generate two distinct primes p and q.Compute n=pq and φ=(p-1)(q-1).<br>Find an integer e, 1&lt;e&lt;φ, such that gcd(e,φ)=1.
A message in this system is a number in the interval [0,n-1].<br>A text to be encrypted is then somehow converted to messages (numbers in the interval [0,n-1]).<br>To encrypt the text,  for each message, m, c=m^e mod n is calculated.
To decrypt the text, the following procedure is needed: calculate d such that ed=1 mod φ, then for each encrypted message, c, calculate m=c^d mod n.
There exist values of e and m  such that m^e mod n=m.<br>We call messages m for which m^e mod n=m unconcealed messages.
An issue when choosing e is that there should not be too many unconcealed messages.<br>For instance, let p=19 and q=37.<br>Then n=19*37=703 and φ=18*36=648.<br>If we choose e=181, then, although gcd(181,648)=1 it turns out that all possible messages<br> m (0≤m≤n-1) are unconcealed when calculating m^e mod n.<br>For any valid choice of e there exist some unconcealed messages.<br>It’s important that the number of unconcealed messages is at a minimum.
Choose p=1009 and q=3643.<br>Find the sum of all values of e, 1&lt;e&lt;φ(1009,3643) and gcd(e,φ)=1, so that the number of unconcealed messages for this value of e is at a minimum.


## 解决方案


## 代码


