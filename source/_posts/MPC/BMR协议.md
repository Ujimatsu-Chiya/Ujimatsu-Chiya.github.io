---
title: BMR协议
date: 2022-03-28 14:26:04
tags: 
  - MPC
mathjax: true
---
<escape><!-- more --></escape>

# BMR 协议

现在有一个实现实现函数$\mathcal{F}$的布尔电路$\mathcal{C}$。
令$F:\{0,1\}^m\rightarrow\{0,1\}^{n\cdot m+1}$为一个$\mathrm{PRG}$。

有$n$个参与方，其中第$j$个参与方的输入为$x_j\in\{0,1\}$。

协议过程：

对于电路中的每一条线$w_i$，每一方$P_j$，都对每一个输入值$b\in\{0,1\}$，随机生成一个子标记$w_{i,j}^b=k_{i,j}^b || p_{i,j}^b\in\{0,1\}^{m+1}$，其中满足$p_{i,j}^b=1-p_{i,j}^{1-b}$。

对于电路中的每一条线$w_i$，每一方$P_j$，都生成一个输入分享$f_{i,j}\in \{0,1\}$。

定义每一方的MPC输入：
$I_{i,j}=[F(w_{i,j}^0),F(w_{i,j}^1),p_{i,j}^0,f_{i,j}]$。

将所有的$I_{i,j},x_j$作为新的输入。

对于每一个门$G$中实现的函数$g$，假设其有两条输入线$w_a,w_b$，输出线为$w_c$。

计算$p_a^0=\bigoplus_{j=1}^np_{a,j}^0,p_b^0=\bigoplus_{j=1}^np_{b,j}^0,p_c^0=\bigoplus_{j=1}^np_{c,j}^0$。

计算$p_a^1=1-p_a^0,p_b^1=1-p_b^0,p_c^1=1-p_c^0$。

计算$f_a=\bigoplus_{j=1}^nf_{a,j},f_b=\bigoplus_{j=1}^nf_{b,j},f_c=\bigoplus_{j=1}^nf_{c,j}$。

接下来创造乱码电路表，对于任意的$2^2$种组合，对于所有的$v_a,v_b\in\{0,1\}$，设$v_c=g(v_a,v_b)$，计算

$$e_{v_a,v_b}=w_c^{v_c\bigoplus f_c}\bigoplus\bigoplus_{j=1}^n[F(w_{a,j}^{v_a\bigoplus f_a})\bigoplus F(w_{b,j}^{v_b\bigoplus f_b})]$$

值$e_{v_a,v_b}$放在位置$(p_a^{v_a},p_b^{v_b})$。

其中，$w_c^0=w_{c,1}^0||w_{c,2}^0||\cdots||w_{c,n}^0||p_c^0,w_c^1=w_{c,1}^1||w_{c,2}^1||\cdots||w_{c,n}^1||p_c^1$。

根据给定的$x_1,x_2,\cdots,x_n$交付给任意一方解密即可。最终需要揭露每一个值$f_{i,j}$。
