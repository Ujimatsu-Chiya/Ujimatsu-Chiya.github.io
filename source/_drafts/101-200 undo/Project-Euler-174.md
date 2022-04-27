---
title: Project Euler 174
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 174
## 题目
### Counting the number of "hollow" square laminae that can form one, two, three, ... distinct arrangements

We shall define a square lamina to be a square outline with a square "hole" so that the shape possesses vertical and horizontal symmetry.
Given eight tiles it is possible to form a lamina in only one way: 3x3 square with a 1x1 hole in the middle. However, using thirty-two tiles it is possible to form two distinct laminae.
<div class="center">
<img src="project/images/p173_square_laminas.gif" alt="" />

# Project Euler 174
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
  
<b>Counting the number of “hollow” square laminae that can form one, two, three, \dots distinct arrangements</b>
We shall define a square lamina to be a square outline with a square “hole” so that the shape possesses vertical and horizontal symmetry.
Given eight tiles it is possible to form a lamina in only one way: 3x3 square with a 1x1 hole in the middle. However, using thirty-two tiles it is possible to form two distinct laminae.
<center><img src="https://projecteuler.net/project/images/p173_square_laminas.gif" alt=""></center>

If t represents the number of tiles used, we shall say that t = 8 is type L(1) and t = 32 is type L(2).
Let N(n) be the number of t ≤ 1000000 such that t is type L(n); for example, N(15) = 832.
What is ∑ N(n) for 1 ≤ n ≤ 10?


## 解决方案


## 代码


