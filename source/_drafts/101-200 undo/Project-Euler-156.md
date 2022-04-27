---
title: Project Euler 156
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 156
## 题目
### Counting Digits

Starting from zero the natural numbers are written down in base 10 like this:
<br />
0 1 2 3 4 5 6 7 8 9 10 11 12\dots.

Consider the digit <var>d</var>=1. After we write down each number <var>n</var>, we will update the number of ones that have occurred and call this number <var>f</var>(<var>n</var>,1). The first values for <var>f</var>(<var>n</var>,1), then, are as follows:
<div class="center">
<table class="center" align="center"><tr><td><var>n</var></td><td><var>f</var>(<var>n</var>,1)</td>
</tr><tr><td>0</td><td>0</td>
</tr><tr><td>1</td><td>1</td>
</tr><tr><td>2</td><td>1</td>
</tr><tr><td>3</td><td>1</td>
</tr><tr><td>4</td><td>1</td>
</tr><tr><td>5</td><td>1</td>
</tr><tr><td>6</td><td>1</td>
</tr><tr><td>7</td><td>1</td>
</tr><tr><td>8</td><td>1</td>
</tr><tr><td>9</td><td>1</td>
</tr><tr><td>10</td><td>2</td>
</tr><tr><td>11</td><td>4</td>
</tr><tr><td>12</td><td>5</td>
</tr></table>

# Project Euler 156
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
  
<b>Counting Digits</b>
Starting from zero the natural numbers are written down in base 10 like this:<br>0 1 2 3 4 5 6 7 8 9 10 11 12\dots.
Consider the digit d=1. After we write down each number n, we will update the number of ones that have occurred and call this number f(n,1). The first values for f(n,1), then, are as follows:
<table>
<thead>
<tr>
<th align="center">n</th>
<th align="center">f(n,1)</th>
</tr>
</thead>
<tbody><tr>
<td align="center">0</td>
<td align="center">0</td>
</tr>
<tr>
<td align="center">1</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">2</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">3</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">4</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">5</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">6</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">7</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">8</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">9</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">10</td>
<td align="center">2</td>
</tr>
<tr>
<td align="center">11</td>
<td align="center">4</td>
</tr>
<tr>
<td align="center">12</td>
<td align="center">5</td>
</tr>
</tbody></table>
Note that f(n,1) never equals 3.<br>So the first two solutions of the equation f(n,1)=n are n=0 and n=1. The next solution is n=199981.
In the same manner the function f(n,d) gives the total number of digits d that have been written down after the number n has been written.<br>In fact, for every digit d ≠ 0, 0 is the first solution of the equation f(n,d)=n.
Let s(d) be the sum of all the solutions for which f(n,d)=n.<br>You are given that s(1)=22786974071.
Find  ∑ s(d) for 1 ≤ d ≤ 9.
Note: if, for some n, f(n,d)=n for more than one value of d this value of n is counted again for every value of d for which f(n,d)=n.


## 解决方案


## 代码


