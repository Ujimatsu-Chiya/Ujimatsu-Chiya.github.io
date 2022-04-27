---
title: Project Euler 154
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 154
## 题目
### Exploring Pascal's pyramid

A triangular pyramid is constructed using spherical balls so that each ball rests on exactly three balls of the next lower level.
<div class="center"><img src="project/images/p154_pyramid.png" class="dark_img" alt="" />

# Project Euler 154
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
  
<b>Exploring Pascal’s pyramid</b>
A triangular pyramid is constructed using spherical balls so that each ball rests on exactly three balls of the next lower level.
<center><img src="https://projecteuler.net/project/images/p154_pyramid.gif" width="488" height="379" alt=""></center>

Then, we calculate the number of paths leading from the apex to each position:
A path starts at the apex and progresses downwards to any of the three spheres directly below the current position.
Consequently, the number of paths to reach a certain position is the sum of the numbers immediately above it (depending on the position, there are up to three numbers above it).
The result is <em>Pascal’s pyramid</em> and the numbers at each level n are the coefficients of the trinomial expansion<br>(x + y + z)^n.
How many coefficients in the expansion of (x + y + z)^200000 are multiples of 10^12?


## 解决方案


## 代码


