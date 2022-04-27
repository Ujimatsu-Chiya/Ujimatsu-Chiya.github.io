---
title: Project Euler 167
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 167
## 题目
### Investigating Ulam sequences

For two positive integers a and b, the Ulam sequence U(a,b) is defined by U(a,b)_1 = a, U(a,b)_2 = b and for k &gt; 2,
U(a,b)_k is the smallest integer greater than U(a,b)_(k-1) which can be written in exactly one way as the sum of two distinct previous members of U(a,b).
For example, the sequence U(1,2) begins with<br />
1, 2, 3 = 1 + 2, 4 = 1 + 3, 6 = 2 + 4, 8 = 2 + 6, 11 = 3 + 8;<br />
5 does not belong to it because 5 = 1 + 4 = 2 + 3 has two representations as the sum of two previous members, likewise 7 = 1 + 6 = 3 + 4.
Find <span style="font-size:larger;"><span style="font-size:larger;">∑</span></span> U(2,2<var>n</var>+1)_<var>k</var> for 2 ≤ <var>n</var> ≤10, where <var>k</var> = 10^11.


# Project Euler 167
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
  
<b>Investigating Ulam sequences</b>
For two positive integers a and b, the Ulam sequence U(a,b) is defined by U(a,b)_1 = a, U(a,b)_2 = b and for k &gt; 2,<br>U(a,b)_k is the smallest integer greater than U(a,b)_(k-1) which can be written in exactly one way as the sum of two distinct previous members of U(a,b).
For example, the sequence U(1,2) begins with<br>1, 2, 3 = 1 + 2, 4 = 1 + 3, 6 = 2 + 4, 8 = 2 + 6, 11 = 3 + 8;<br>5 does not belong to it because 5 = 1 + 4 = 2 + 3 has two representations as the sum of two previous members, likewise 7 = 1 + 6 = 3 + 4.
Find ∑U(2,2n+1)_k for 2 ≤ n ≤10, where k = 10^11.


## 解决方案


## 代码


