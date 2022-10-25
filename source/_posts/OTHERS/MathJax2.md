---
title: MathJax实例
mathjax: true
category:
  - MathJax
date: 2022-08-14 22:11:41
tags:
---

<escape><!-- more --></escape>

本篇文章基于MathJax编写了$15$个实例，尽量涵盖了各种常用符号，以熟悉各种符号的用法。

## 扩展欧几里得算法（Python）

```latex
$\begin{aligned}
& \texttt{def ex_gcd(a, b):}\\
& \qquad \texttt{if b == 0: }\\
& \qquad \qquad \texttt{return 1, 0, a}\\
& \qquad \texttt{else: }\\
& \qquad \qquad \texttt{x, y, g = ex_gcd(b, a % b)}\\
& \qquad \qquad \texttt{return y, x - (a // b) * y, g}\\
\\
\\
& \texttt{N = 5}\\
& \texttt{for n in range(1, N + 1):}\\
& \qquad \texttt{for m in range(1, N + 1):}\\
& \qquad \qquad \texttt{print(ex_gcd(n, m))}
\end{aligned}$
```

$\begin{aligned}
& \texttt{def ex_gcd(a, b):}\\
& \qquad \texttt{if b == 0: }\\
& \qquad \qquad \texttt{return 1, 0, a}\\
& \qquad \texttt{else: }\\
& \qquad \qquad \texttt{x, y, g = ex_gcd(b, a % b)}\\
& \qquad \qquad \texttt{return y, x - (a // b) * y, g}\\
\\
\\
& \texttt{N = 5}\\
& \texttt{for n in range(1, N + 1):}\\
& \qquad \texttt{for m in range(1, N + 1):}\\
& \qquad \qquad \texttt{print(ex_gcd(n, m))}
\end{aligned}$

## 范德蒙德行列式

```latex
$$\begin{vmatrix}
1   & 1   & \dots & 1\\
x_1 & x_2 & \dots & x_n\\
\vdots & \vdots & \ddots & \vdots\\
x_1^{n-1} & x_2^{n-2} & \dots & x_n^{n-1}
\end{vmatrix} = \prod_{1\le j\le i\le n} (x_i-x_j)$$
```

$$\det \begin{bmatrix}
1   & 1   & \dots & 1\\
x_1 & x_2 & \dots & x_n\\
\vdots & \vdots & \ddots & \vdots\\
x_1^{n-1} & x_2^{n-2} & \dots & x_n^{n-1}
\end{bmatrix} = \prod_{1\le j\le i\le n} (x_i-x_j)$$

## 碳酸氢钙溶液加热

```latex
$$\mathrm{Ca(HCO_3)_2\xrightarrow{\triangle}CaCO_3\downarrow+CO_2\uparrow+H_2O}$$
```

$$\mathrm{Ca(HCO_3)_2\xrightarrow{\triangle}CaCO_3\downarrow+CO_2\uparrow+H_2O}$$

## 薛定谔方程

```latex
$$i\hbar\dfrac{\partial}{\partial t}|\psi (t)\rangle = \hat{H}|\psi(t)\rangle$$

$$i\hbar\dfrac{\partial}{\partial t}\Psi (x,t) = \left[-\dfrac{\hbar^2}{2m}\dfrac{\partial^2}{\partial x^2}+V(x,t)\right]\Psi(x,t)$$
```

$$i\hbar\dfrac{\partial}{\partial t}|\psi (t)\rangle = \hat{H}|\psi(t)\rangle$$

$$i\hbar\dfrac{\partial}{\partial t}\Psi (x,t) = \left[-\dfrac{\hbar^2}{2m}\dfrac{\partial^2}{\partial x^2}+V(x,t)\right]\Psi(x,t)$$

## 麦克斯韦方程组

```latex
$$\begin{cases}
\nabla \cdot \mathbf{E} = \dfrac{\rho}{\varepsilon_0} & \text{Gauss's law}\\
\nabla \cdot \mathbf{B}=0 & \text{Gauss's law for magnetism}\\
\nabla \times \mathbf{E} = -\dfrac{\partial\mathbf{B}}{\partial t} & \text{Maxwell–Faraday equation}\\
\nabla \times \mathbf{B} =  \mu_0 \left(\mathbf{J} + \varepsilon_0\dfrac{\partial \mathbf{E}}{\partial t}\right) & \text{Ampère's circuital law}
\end{cases}$$
```

$$\begin{cases}
\nabla \cdot \mathbf{E} = \dfrac{\rho}{\varepsilon_0} & \text{Gauss's law}\\
\nabla \cdot \mathbf{B}=0 & \text{Gauss's law for magnetism}\\
\nabla \times \mathbf{E} = -\dfrac{\partial\mathbf{B}}{\partial t} & \text{Maxwell–Faraday equation}\\
\nabla \times \mathbf{B} =  \mu_0 \left(\mathbf{J} + \varepsilon_0\dfrac{\partial \mathbf{E}}{\partial t}\right) & \text{Ampère's circuital law}
\end{cases}$$

## 异或运算$S=x \oplus y$的真值表

```latex
$$\begin{array}{|l|l|l|}
\hline
x & y & S\\
\hdashline
0 & 0 & 0\\
\hline
0 & 1 & 1\\
\hline
1 & 0 & 1\\
\hline
1 & 0 & 0\\
\hline
\end{array}$$
```

$$\begin{array}{|l|l|l|}
\hline
x & y & S\\
\hdashline
0 & 0 & 0\\
\hline
0 & 1 & 1\\
\hline
1 & 0 & 1\\
\hline
1 & 0 & 0\\
\hline
\end{array}$$

## 狄利克雷函数

```latex
$$ \mathbf{1}_{\mathbb{Q}}(x)=
{\begin{cases}
1&x\in \mathbb {Q} \\
0&x\notin \mathbb {Q}
\end{cases}}$$
```

$$ \mathbf{1}_{\mathbb{Q}}(x)=
{\begin{cases}
1&x\in \mathbb {Q} \\
0&x\notin \mathbb {Q}
\end{cases}}$$

## 雅可比符号

```latex
$$\left(\dfrac{a}{p}\right) =
\begin{cases}
0 & \text{if $a\equiv 0\pmod{p}$}\\
1 & \text{if }a\not\equiv 0\pmod p \wedge \exists  x: x^2\equiv a\pmod p \\
-1 & \text{if }a\not\equiv 0\pmod p \wedge \nexists  x: x^2\equiv a\pmod p
\end{cases}$$
```

$$\left(\dfrac{a}{p}\right) =
\begin{cases}
0 & \text{if $a\equiv 0\pmod{p}$}\\
1 & \text{if }a\not\equiv 0\pmod p \wedge \exists  x: x^2\equiv a\pmod p \\
-1 & \text{if }a\not\equiv 0\pmod p \wedge \nexists  x: x^2\equiv a\pmod p
\end{cases}$$

## 斯托克斯公式

```latex
$$\oint_{\Gamma}Pdx+Qdy+Rdz=\iint_{\Sigma}\left(\dfrac{\partial R}{\partial y}-\dfrac{\partial Q}{\partial z}\right) dydz+\left(\dfrac{\partial P}{\partial z}-\dfrac{\partial R}{\partial x}\right) dzdx+\left(\dfrac{\partial Q}{\partial x}-\dfrac{\partial P}{\partial y}\right) dxdy$$
```

$$\oint_{\Gamma}Pdx+Qdy+Rdz=\iint_{\Sigma}\left(\dfrac{\partial R}{\partial y}-\dfrac{\partial Q}{\partial z}\right) dydz+\left(\dfrac{\partial P}{\partial z}-\dfrac{\partial R}{\partial x}\right) dzdx+\left(\dfrac{\partial Q}{\partial x}-\dfrac{\partial P}{\partial y}\right) dxdy$$

## $\Gamma$函数与黎曼$\zeta$函数

```latex
$$\begin{aligned}
\Gamma(z)=&\int_{0}^{\infty} t^{z-1} \mathrm{e}^{-t}dt &\\
\zeta(s)=&\sum_{n=1}^{\infty} \dfrac{1}{n^s}
\end{aligned}$$
```

$$\begin{aligned}
\Gamma(z)=&\int_{0}^{\infty} t^{z-1} \mathrm{e}^{-t}dt &\\
\zeta(s)=&\sum_{n=1}^{\infty} \dfrac{1}{n^s}
\end{aligned}$$

## 德摩根律

```latex
$$\begin{align}
& \neg (P\lor Q)\Longleftrightarrow \neg P\land\neg Q \tag{propositional logic}\\
& \neg (P\land Q)\Longleftrightarrow \neg P\lor\neg Q \\
& (A \cup B)^{\complement}=A^{\complement}\cap B^{\complement} \tag{set theory}\\
& (A \cap B)^{\complement}=A^{\complement}\cup B^{\complement} \\
& \overline{A\cup B}=\overline{A}\cap\overline{B} \tag{probability theory}\\
& \overline{A\cap B}=\overline{A}\cup\overline{B}
\end{align}$$
```

$$\begin{align}
& \neg (P\lor Q)\Longleftrightarrow \neg P\land\neg Q \tag{propositional logic}\\
& \neg (P\land Q)\Longleftrightarrow \neg P\lor\neg Q \\
& (A \cup B)^{\complement}=A^{\complement}\cap B^{\complement} \tag{set theory}\\
& (A \cap B)^{\complement}=A^{\complement}\cup B^{\complement} \\
& \overline{A\cup B}=\overline{A}\cap\overline{B} \tag{probability theory}\\
& \overline{A\cap B}=\overline{A}\cup\overline{B}
\end{align}$$

## 贝叶斯公式

```latex
$$P(A_i|B)=\dfrac{P(B|A_i)\cdot P(A_i)}{\sum_{j=1}^n P(B|A_j)\cdot P(A_j)}$$
```

$$P(A_i|B)=\dfrac{P(B|A_i)\cdot P(A_i)}{\sum_{j=1}^n P(B|A_j)\cdot P(A_j)}$$

## 麦克劳林级数

```latex
$$\begin{align}
&e^x=\sum_{n=0}^{\infty} \dfrac{x^n}{n!}\\
&\sin x = \sum_{n=0}^{\infty} (-1)^n\dfrac{x^{2n+1}}{(2n+1)!}\\
&\cos x = \sum_{n=0}^{\infty} (-1)^n\dfrac{x^{2n}}{(2n)!}\\
&\ln(x+1) = \sum_{n=0}^{\infty} (-1)^n\dfrac{x^{n+1}}{(n+1)!}\\
\end{align}$$
```

$$\begin{align}
&e^x=\sum_{n=0}^{\infty} \dfrac{x^n}{n!}\\
&\sin x = \sum_{n=0}^{\infty} (-1)^n\dfrac{x^{2n+1}}{(2n+1)!}\\
&\cos x = \sum_{n=0}^{\infty} (-1)^n\dfrac{x^{2n}}{(2n)!}\\
&\ln(x+1) = \sum_{n=0}^{\infty} (-1)^n\dfrac{x^{n+1}}{(n+1)!}\\
\end{align}$$

## 自然对数$e$的定义

```latex
$$e=\lim_{x\rightarrow\infty}\left(1+\dfrac{1}{x}\right)^x$$
```

$$e=\lim_{x\rightarrow\infty}\left(1+\dfrac{1}{x}\right)^x$$

## 二项式定理

```latex
$$(x+y)^n=\sum_{k=0}^n \dbinom{n}{k} x^ky^{n-k}$$
```

$$(x+y)^n=\sum_{k=0}^n \dbinom{n}{k} x^ky^{n-k}$$
