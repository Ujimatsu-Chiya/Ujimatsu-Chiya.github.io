---
title: GMW协议
date: 2022-03-28 14:26:05
tags: 
  - MPC
katex: true
---
<escape><!-- more --></escape>

# GMW协议

## 输入

$P_1:x\in\{0,1\}$

$P_2:y\in\{0,1\}$

## 输出

$x \bigoplus y,x\bigwedge y.$

## 协议

$r\in\{0,1\}$由$P_1$生成，发送给$P_2$

$s\in\{0,1\}$由$P_2$生成，发送给$P_1$

$S_i^1=x \bigoplus r$

$S_i^2=r$

$S_j^2=y \bigoplus s$

$S_j^1=s$

$S_k^1=S_i^1\bigoplus S_j^1$

$S_k^2=S_i^2\bigoplus S_j^2$

$S_k^1\bigoplus S_k^2=(S_i^1 \bigoplus S_j^1) \bigoplus (s_i^2\bigoplus s_j^2)=x \bigoplus y$

$P_1$暴露分享$S_k^1$，$P_2$暴露分享$S_k^2$即可计算$x \bigoplus y$。

令$F(S_i^2,S_j^2)=(S_i^1\bigoplus S_i^2)\bigwedge(S_i^2\bigoplus S_j^2)=x\bigwedge y$

$b\in \{0,1\}$由$P_1$随机生成。

$P_1$预先计算好$F$的四种可能性$F(0,0),F(0,1),F(1,0),F(1,1)$。
和$P_2$进行1-out-of-4-OT：
$$ OT_1^4=\left\{
\begin{aligned}
b \bigoplus F(0,0) \\
b \bigoplus F(0,1) \\
b \bigoplus F(1,0) \\
b \bigoplus F(1,1) \\
\end{aligned}
\right.
$$
其中$P_2$提供$(S_i^2,S_j^2)$的值，得到的值为$b\bigoplus F(S_i^2,S_j^2)$。

$P_1$暴露分享$b$，$P_2$暴露分享$b\bigoplus F(S_i^2,S_j^2)$即可计算$x \bigwedge y$。
