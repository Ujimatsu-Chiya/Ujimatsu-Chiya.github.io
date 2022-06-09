---
title: BGW协议
date: 2022-03-28 14:26:03
tags: 
  - MPC
mathjax: true
---
<escape><!-- more --></escape>

# BGW 协议

$v\in \Bbb{F}$，其中$[v]$是各方持有的Shamir秘密分享。

选定一个多项式$p$，其次数最高为$t$，其中$p(0)=v$。

$P_i$方所持有的份额为$p(i)$。

$t$：共享阈值。任何$t$共享的集合都不会显示有关$v$的信息。

各方都持有该线路上值$v_w$的秘密共享$[v_w]$。

## 输入

$v_\alpha,v_\beta \in \Bbb{F}$，其中$\Bbb{F}$是一个域。

## 输出

$v_\gamma=v_\alpha\circ v_\beta$。

## 协议

构造两个多项式$p$和$q$用于生成shamir秘密共享，那么$P_i$得到的秘密共享为$(i,p_\alpha(i),p_\beta(i))$，$[v_\alpha]$指的是任一$p_\alpha(i)$，$[v_\beta]$指的是任一$p_\beta(i)$。

### $v_\gamma=v_\alpha+v_\beta$

计算参与方取出共享$[v_\alpha]$和$[v_\beta]$，计算加法共享$[v_\gamma]=[v_\alpha+v_\beta]$。将每一方的分享$[v_\gamma]$一同还原即可得到$v_\alpha+v_\beta$的值。

### $v_\gamma=c \cdot v_\alpha$

$c$是一个整数。

计算参与方取出共享$[v_\alpha]$，计算加法共享$[v_\gamma]=[c \cdot v_\alpha]$。将每一方的分享$[v_\gamma]$一同还原即可得到$c \cdot v_\alpha$的值。

### $v_\gamma=v_\alpha\cdot v_\beta$

令$q=p_\alpha\cdot p_\beta$

对于每一方而言，将它拥有的两个分享$p_\alpha(i),p_\beta(i)$相乘，得到一个新分享$(i,q(i))$。

目前需要基于这$n$个分享重新进行$2t$次的多项式插值：

$$v_\alpha\cdot v_\beta=\sum_{k=1}^{2t+1}\lambda_kq(k)$$

其中$\lambda_i$为拉格朗日常数。

做法：

每一方随机生成一个$t$次多项式，其中$P_i$生成的多项式为$r_i$，常系数项为$q(i)$。

那么$P_i$就将这个$q(i)$作为秘密，以$(t,n)$-shamir秘密共享方案进行分发。$P_i$发送给$P_j$的秘密为$(j,r_i(j))$

目前每一方$P_i$都掌握以下秘密：值$v_\gamma$的一个分享$(i,q(i))$，任意一方$P_j$的$q(j)$的一个分享$(i,r_j(i)),\forall j \in [1,n]$。

之后通过这些分享，任意$t$方都可以将$n$个$(i,q(i))$重构完成。根据这$n$个$(i,q(i))$可以重新将$2t+1$个$\lambda_k$的值重构完成，从而计算出$v_\alpha\cdot v_\beta$。

这个协议只有在$2t+1\le n$时才安全。

## Beaver 三元组

这种改进是将一系列开销移到了协议开始前。

离线阶段：
通过一些手段生成多个乘法三元组。其中这些$a$和$b$在域$\Bbb{F}$内随机选择，$c=ab$。

在协议前，一系列的shamir分享三元组$([a],[b],[c])$已经分发到各方。

在线阶段：

各方计算$[d]=[v_\alpha-a]$的值，并公开。

各方计算$[e]=[v_\beta-b]$的值，并公开。

由于$[d]$和$[e]$都被公开，因此现在已经得到$d=v_\alpha-a$和$e=v_\beta-b$的值。

由于

$\begin{aligned}
    v_\alpha\cdot v_\beta &=(d+a)\cdot(e+b) \\
    &=de+db+ae+ab\\
    &=de+db+ae+c
\end{aligned}$

故各方计算自己的份额：$[v_\alpha\cdot v_\beta]=de+d[b]+e[a]+[c]$

各方揭露$[v_\alpha\cdot v_\beta]$，完成计算。
