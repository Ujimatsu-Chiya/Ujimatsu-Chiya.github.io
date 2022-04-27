---
title: Project Euler 153
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 153
## 题目
### Investigating Gaussian Integers

As we all know the equation <var>x</var>^2=-1 has no solutions for real <var>x</var>.
<br />
If we however introduce the imaginary number <var>i</var> this equation has two solutions: <var>x=i</var> and <var>x=-i</var>.
<br />
If we go a step further the equation (<var>x</var>-3)^2=-4 has two complex solutions: <var>x</var>=3+2<var>i</var> and <var>x</var>=3-2<var>i</var>.
<br /><var>x</var>=3+2<var>i</var> and <var>x</var>=3-2<var>i</var> are called each others' complex conjugate.
<br />
Numbers of the form <var>a</var>+<var>bi</var> are called complex numbers.
<br />
In general <var>a</var>+<var>bi</var> and <var>a</var>−<var>bi</var> are each other's complex conjugate.
A Gaussian Integer is a complex number <var>a</var>+<var>bi</var> such that both <var>a</var> and <var>b</var> are integers.
<br />
The regular integers are also Gaussian integers (with <var>b</var>=0).
<br />
To distinguish them from Gaussian integers with <var>b</var> ≠ 0 we call such integers "rational integers."
<br />
A Gaussian integer is called a divisor of a rational integer <var>n</var> if the result is also a Gaussian integer.
<br />
If for example we divide 5 by 1+2<var>i</var> we can simplify $\dfrac{5}{1 + 2i}$ in the following manner:
<br />
Multiply numerator and denominator by the complex conjugate of 1+2<var>i</var>: 1−2<var>i</var>.
<br />
The result is $\dfrac{5}{1 + 2i} = \dfrac{5}{1 + 2i}\dfrac{1 - 2i}{1 - 2i} = \dfrac{5(1 - 2i)}{1 - (2i)^2} = \dfrac{5(1 - 2i)}{1 - (-4)} = \dfrac{5(1 - 2i)}{5} = 1 - 2i$.
<br />
So 1+2<var>i</var> is a divisor of 5.
<br />
Note that 1+<var>i</var> is not a divisor of 5 because $\dfrac{5}{1 + i} = \dfrac{5}{2} - \dfrac{5}{2}i$.
<br />
Note also that if the Gaussian Integer (<var>a</var>+<var>bi</var>) is a divisor of a rational integer <var>n</var>, then its complex conjugate (<var>a</var>−<var>bi</var>) is also a divisor of <var>n</var>.
In fact, 5 has six divisors such that the real part is positive: {1, 1 + 2<var>i</var>, 1 − 2<var>i</var>, 2 + <var>i</var>, 2 − <var>i</var>, 5}.
<br />
The following is a table of all of the divisors for the first five positive rational integers:
<table align="center" border="1"><tr><td width="20">
<var>n</var></td><td> Gaussian integer divisors<br />
with positive real part</td><td>Sum s(<var>n</var>) of <br />these

divisors</td></tr><tr><td>1</td><td>1</td><td>1</td>
</tr><tr><td>2</td><td>1, 1+<var>i</var>, 1-<var>i</var>, 2</td><td>5</td>
</tr><tr><td>3</td><td>1, 3</td><td>4</td>
</tr><tr><td>4</td><td>1, 1+<var>i</var>, 1-<var>i</var>, 2, 2+2<var>i</var>, 2-2<var>i</var>,4</td><td>13</td>
</tr><tr><td>5</td><td>1, 1+2<var>i</var>, 1-2<var>i</var>, 2+<var>i</var>, 2-<var>i</var>, 5</td><td>12</td>
</tr></table>For divisors with positive real parts, then, we have: $\sum \limits_{n = 1}^{5} {s(n)} = 35$.
For $\sum \limits_{n = 1}^{10^5} {s(n)} = 17924657155$.
What is $\sum \limits_{n = 1}^{10^8} {s(n)}$?


# Project Euler 153
## 题目
### YPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=2">
<meta name="theme-color" content="#222">
<meta name="generator" content="Hexo 4.2.1">
  <link rel="icon" type="image/png" sizes="32x32" href="/images/32x32.png">
  <link rel="icon" type="image/png" sizes="16x16" href="/images/16x16.png">

<link rel="stylesheet" href="/css/main.css">

<link rel="stylesheet" href="//fonts.googleapis.com/css?family=Lato:300,300italic,400,400italic,700,700italic|Lato', 'Microsoft Yahei Light:300,300italic,400,400italic,700,700italic|Cambria', 'Microsoft Yahei Light:300,300italic,400,400italic,700,700italic|Verdana', Lato, 'Microsoft Yahei Light:300,300italic,400,400italic,700,700italic&display=swap&subset=latin,latin-ext">
<link rel="stylesheet" href="/lib/font-awesome/css/all.min.css">

<script id="hexo-configurations">
    var NexT = window.NexT || {};
    var CONFIG = {"hostname":"yoursite.com","root":"/","scheme":"Mist","version":"7.8.0","exturl":false,"sidebar":{"position":"right","display":"hide","padding":18,"offset":12,"onmobile":false},"copycode":{"enable":false,"show_result":false,"style":null},"back2top":{"enable":true,"sidebar":false,"scrollpercent":false},"bookmark":{"enable":false,"color":"#222","save":"auto"},"fancybox":false,"mediumzoom":false,"lazyload":false,"pangu":false,"comments":{"style":"tabs","active":null,"storage":true,"lazyload":false,"nav":null},"algolia":{"hits":{"per_page":10},"labels":{"input_placeholder":"Search for Posts","hits_empty":"We didn't find any results for the search: ${query}","hits_stats":"${hits} results found in ${time} ms"}},"localsearch":{"enable":true,"trigger":"auto","top_n_per_article":1,"unescape":false,"preload":false},"motion":{"enable":true,"async":false,"transition":{"post_block":"fadeIn","post_header":"slideDownIn","post_body":"slideDownIn","coll_header":"slideLeftIn","sidebar":"slideUpIn"}},"path":"search.xml"};
  
<b>Investigating Gaussian Integers</b>
As we all know the equation x^2=-1 has no solutions for real x.<br>If we however introduce the imaginary number i this equation has two solutions: x=i and x=-i.<br>If we go a step further the equation (x-3)^2=-4 has two complex solutions: x=3+2i and x=3-2i.<br>x=3+2i and x=3-2i are called each others’ complex conjugate.<br>Numbers of the form a+bi are called complex numbers.<br>In general a+bi and a−bi are each other’s complex conjugate.
A Gaussian Integer is a complex number a+bi such that both a and b are integers.<br>The regular integers are also Gaussian integers (with b=0).<br>To distinguish them from Gaussian integers with b ≠ 0 we call such integers “rational integers.”<br>A Gaussian integer is called a divisor of a rational integer n if the result is also a Gaussian integer.<br>If for example we divide 5 by 1+2i we can simplify $\frac{5}{1+2i}$ in the following manner:<br>Multiply numerator and denominator by the complex conjugate of 1+2i: 1−2i.<br>The result is $\frac{5}{1+2i}=\frac{5}{1+2i}\frac{1-2i}{1-2i}=\frac{5(1-2i)}{1-(2i)^2}=\frac{5(1-2i)}{1-(-4)}=\frac{5(1-2i)}{5}=1-2i$.<br>So 1+2i is a divisor of 5.<br>Note that 1+i is not a divisor of 5 because $\frac{5}{1+i}=\frac{5}{2}-\frac{5}{2}i$.<br>Note also that if the Gaussian Integer (a+bi) is a divisor of a rational integer n, then its complex conjugate (a−bi) is also a divisor of n.
In fact, 5 has six divisors such that the real part is positive: {1, 1 + 2i, 1 − 2i, 2 + i, 2 − i, 5}.<br>The following is a table of all of the divisors for the first five positive rational integers:
<table>
<thead>
<tr>
<th align="center">n</th>
<th align="center">Gaussian integer divisors with positive real part</th>
<th align="center">Sum s(n) of these divisors</th>
</tr>
</thead>
<tbody><tr>
<td align="center">1</td>
<td align="center">1</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">2</td>
<td align="center">1, 1+i, 1-i, 2</td>
<td align="center">5</td>
</tr>
<tr>
<td align="center">3</td>
<td align="center">1, 3</td>
<td align="center">4</td>
</tr>
<tr>
<td align="center">4</td>
<td align="center">1, 1+i, 1-i, 2, 2+2i, 2-2i,4</td>
<td align="center">13</td>
</tr>
<tr>
<td align="center">5</td>
<td align="center">1, 1+2i, 1-2i, 2+i, 2-i, 5</td>
<td align="center">12</td>
</tr>
</tbody></table>
For divisors with positive real parts, then, we have: $\sum_{n=1}^{5}s(n)=35$.
For 1 ≤ n ≤ 10^5, ∑ s(n)=17924657155.
What is ∑ s(n) for 1 ≤ n ≤ 10^8?


## 解决方案


## 代码


