---
title: MathJax数学符号
mathjax: true
category:
  - MathJax
date: 2022-08-14 22:11:32
tags:
---

<escape><!-- more --></escape>

本篇文章简要地列出了MathJax中的所有符号（可能不全），并按照形状进行分类。

## 区间形状

|区间类型|代码|
|-|-|
|$\langle\rangle$|`\langle\rangle`|
|$\lfloor\rfloor$|`\lfloor\rfloor`|
|$\lceil\rceil$|`\lceil\rceil`|
|$()$|`()`|
|$[]$|`[]`|
|$\{\}$|`\{\}`|
|$\lmoustache\rmoustache$|`\lmoustache\rmoustache`|
|$\lvert\rvert$|`\lvert\rvert`|
|$\lVert\rVert$|`\lVert\rVert`|
|$\lgroup\rgroup$|`\lgroup\rgroup`|

## 希腊字母

|大写||小写||
|-|-|-|-|
|$A$|`A`|$\alpha$|`\alpha`|
|$B$|`B`|$\beta$|`\beta`|
|$\Gamma,\varGamma$|`\Gamma,\varGamma`|$\gamma$|`\gamma`|
|$\Delta,\varDelta$|`\Delta,\varDelta`|$\delta$|`\delta`|
|$E$|`E`|$\epsilon,\varepsilon$|`\epsilon,\varepsilon`|
|$Z$|`Z`|$\zeta$|`\zeta`|
|$H$|`H`|$\eta$|`\eta`|
|$\Theta,\varTheta$|`\Theta,\varTheta`|$\theta,\vartheta$|`\theta,\vartheta`|
|$I$|`I`|$\iota$|`\iota`|
|$K$|`K`|$\kappa,\varkappa$|`\kappa,\varkappa`|
|$\Lambda,\varLambda$|`\Lambda,\varLambda`|$\lambda$|`\lambda`|
|$M$|`M`|$\mu$|`\mu`|
|$N$|`N`|$\nu$|`\nu`|
|$\Xi,\varXi$|`\Xi,\varXi`|$\xi$|`\xi`|
|$O$|`O`|$\omicron$|`\omicron`|
|$\Pi,\varPi$|`\Pi,\varPi`|$\pi,\varpi$|`\pi,\varpi`|
|$P$|`P`|$\rho,\varrho$|`\rho,\varrho`|
|$\Sigma,\varSigma$|`\Sigma,\varSigma`|$\sigma,\varsigma$|`\sigma,\varsigma`|
|$T$|`T`|$\tau$|`\tau`|
|$\Upsilon,\varUpsilon$|`\Upsilon,\varUpsilon`|$\upsilon$|`\upsilon`|
|$\Phi,\varPhi$|`\Phi,\varPhi`|$\phi,\varphi$|`\phi,\varphi`|
|$X$|`X`|$\chi$|`\chi`|
|$\Psi,\varPsi$|`\Psi,\varPsi`|$\psi$|`\psi`|
|$\Omega,\varOmega$|`\Omega,\varOmega`|$\omega$|`\omega`|

## 希伯来字母

|||
|-|-|
|$\aleph$|`\aleph`|
|$\beth$|`\beth`|
|$\daleth$|`\daleth`|
|$\gimel$|`\gimel`|

## 字体与注释

使用`\mathxx{}`时，公式中的所有字母将会转换成对应字体。而使用`\textxx{}`时，里面的特殊字符也不会被转义。

|||||
|-|-|-|-|
|$ABCDEFGHIJKLMNOPQRSTUVWXYZ$|$abcdefghijklmnopqrstuvwxyz$|$0123456789$|`原始字体`|
|$\mathrm{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$|$\mathrm{abcdefghijklmnopqrstuvwxyz}$|$\mathrm{0123456789}$|`\mathrm{}`|
|$\mathbf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$|$\mathbf{abcdefghijklmnopqrstuvwxyz}$|$\mathbf{0123456789}$|`\mathbf{}`|
|$\mathbb{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$|$\mathbb{abcdefghijklmnopqrstuvwxyz}$|$\mathbb{0123456789}$|`\mathrm{}`|
|$\mathcal{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$|$\mathcal{abcdefghijklmnopqrstuvwxyz}$|$\mathcal{0123456789}$|`\mathcal{}`|
|$\mathit{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$|$\mathit{abcdefghijklmnopqrstuvwxyz}$|$\mathit{0123456789}$|`\mathit{}`|
|$\mathscr{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$|$\mathscr{abcdefghijklmnopqrstuvwxyz}$|$\mathscr{0123456789}$|`\mathscr{}`|
|$\mathfrak{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$|$\mathfrak{abcdefghijklmnopqrstuvwxyz}$|$\mathfrak{0123456789}$|`\mathfrak{}`|
|$\mathsf{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$|$\mathsf{abcdefghijklmnopqrstuvwxyz}$|$\mathsf{0123456789}$|`\mathsf{}`|
|$\mathtt{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$|$\mathtt{abcdefghijklmnopqrstuvwxyz}$|$\mathtt{0123456789}$|`\mathtt{}`|
|$\text{\alpha in text mode }\alpha$|`\text{}`|
|$\textrm{\alpha in textrm mode }\alpha$|`\textrm{}`|
|$\textbf{\alpha in textbf mode }\alpha$|`\textbf{}`|
|$\textit{\alpha in textit mode }\alpha$|`\textit{}`|
|$\textsf{\alpha in textsf mode }\alpha$|`\textsf{}`|
|$\texttt{\alpha in texttt mode }\alpha$|`\texttt{}`|
|$\boldsymbol{\alpha}\mathbf{\alpha}$|`\boldsymbol{\alpha}\mathbf{\alpha}`|

## 颜色

命令`\color{}{}`中的第一个参数可以是颜色名称，也可以是RGB参数。第二个参数则是正式染色的文字。

|展示|代码|
|-|-|
|$\color{black}{ABCDabcd1234}$|`\color{black}{ABCDabcd1234}`|
|$\color{grey}{ABCDabcd1234}$|`\color{grey}{ABCDabcd1234}`|
|$\color{silver}{ABCDabcd1234}$|`\color{silver}{ABCDabcd1234}`|
|$\color{white}{ABCDabcd1234}$|`\color{white}{ABCDabcd1234}`|
|$\color{maroon}{ABCDabcd1234}$|`\color{maroon}{ABCDabcd1234}`|
|$\color{red}{ABCDabcd1234}$|`\color{red}{ABCDabcd1234}`|
|$\color{yellow}{ABCDabcd1234}$|`\color{yellow}{ABCDabcd1234}`|
|$\color{lime}{ABCDabcd1234}$|`\color{lime}{ABCDabcd1234}`|
|$\color{olive}{ABCDabcd1234}$|`\color{olive}{ABCDabcd1234}`|
|$\color{green}{ABCDabcd1234}$|`\color{green}{ABCDabcd1234}`|
|$\color{teal}{ABCDabcd1234}$|`\color{teal}{ABCDabcd1234}`|
|$\color{auqa}{ABCDabcd1234}$|`\color{auqa}{ABCDabcd1234}`|
|$\color{blue}{ABCDabcd1234}$|`\color{blue}{ABCDabcd1234}`|
|$\color{navy}{ABCDabcd1234}$|`\color{navy}{ABCDabcd1234}`|
|$\color{purple}{ABCDabcd1234}$|`\color{purple}{ABCDabcd1234}`|
|$\color{fuchsia}{ABCDabcd1234}$|`\color{fuchsia}{ABCDabcd1234}`|

## 模算术`\mod`的用法和比较

|展示|代码|
|-|-|
|$x^2\equiv 1(\mod 5)$|`x^2\equiv 1(\mod 5)`|
|$x^2\equiv 1(\bmod 5)$|`x^2\equiv 1(\bmod 5)`|
|$x^2\equiv 1\pmod{5}$|`x^2\equiv 1\pmod{5}`|

## 分数`\frac`的用法和比较

|行内|行间|代码|
|-|-|-|
|$\frac{a-1}{b-1}$|$\displaystyle{\frac{a-1}{b-1}}$|`\frac{a-1}{b-1}`|
|$\cfrac{2}{1+\cfrac{2}{1+\cfrac{2}{1}}}$|$\displaystyle{\cfrac{2}{1+\cfrac{2}{1+\cfrac{2}{1}}}}$|`\cfrac{2}{1+\cfrac{2}{1+\cfrac{2}{1}}}`|
|$\dfrac{a-1}{b-1}$|$\displaystyle{\dfrac{a-1}{b-1}}$|`\dfrac{a-1}{b-1}`|
|$\tfrac{a-1}{b-1}$|$\displaystyle{\tfrac{a-1}{b-1}}$|`\tfrac{a-1}{b-1}`|
|${a-1 \over b-1}$|$\displaystyle{ {a-1 \over b-1} }$|`{a-1 \over b-1}`|

## 组合数`\binom`的用法和比较（附上`\brace`和`\brack`）

|行内|行间|代码|
|-|-|-|
|$\binom{n+1}{m+1}$|$\displaystyle{\binom{n+1}{m+1}}$|`\binom{n+1}{m+1}`|
|${n+1\choose m+1}$|$\displaystyle{ {n+1\choose m+1} }$|`{n+1\choose m+1}`|
|$\dbinom{n+1}{m+1}$|$\displaystyle{\dbinom{n+1}{m+1}}$|`\dbinom{n+1}{m+1}`|
|$\tbinom{n+1}{m+1}$|$\displaystyle{\tbinom{n+1}{m+1}}$|`\tbinom{n+1}{m+1}`|
|${n+1\brack m+1}$|$\displaystyle{ {n+1\brack m+1} }$|`{n+1\brack m+1}`|
|${n+1\brace m+1}$|$\displaystyle{ {n+1\brace m+1} }$|`{n+1\brace m+1}`|

## 方框的用法和比较

|展示|代码|
|-|-|
|$\boxed{x^3+y^3=z^3}$|`\boxed{x^3+y^3=z^3}`|
|$\boxed{abcd 1234}$|`\boxed{abcd 1234}`|
|$\fbox{abcd 1234}$|`\fbox{abcd 1234}`|

## 占位符`\phantom`的用法和比较

|展示|代码|
|-|-|
|$\begin{array}{l}\text{Side Angle Side}\\\text{S}\hphantom{\text{ ide}}\text{A}\hphantom{\text{ngle }}\text{S}\end{array}$|`\begin{array}{l} \text{Side Angle Side} \\ \text{S} \hphantom {\text{ ide}} \text{A} \hphantom{\text{ngle }} \text{S}\end{array}`|
|$\begin{matrix}1&-1\\ \phantom{}\\1&\phantom{-}1\end{matrix}$|`\begin{matrix}1&-1\\ \phantom{}\\1&\phantom{-}1\end{matrix}`|
|$\dbinom{\dfrac ab}c \dbinom{\vphantom{\dfrac ab}}c$|`\dbinom{\dfrac ab}c \dbinom{\vphantom{\dfrac ab}}c`|

## 公式大小

|展示|代码|
|-|-|
|${\tiny AB}$|`{\tiny AB}`|
|${\Tiny AB}$|`{\Tiny AB}`|
|$AB$|`AB`|
|$\large AB$|`\large AB`|
|$\Large AB$|`\Large AB`|
|$\LARGE AB$|`\LARGE AB`|
|${\huge AB}$|`{\huge AB}`|
|${\Huge AB}$|`{\Huge AB}`|

## 其它基本符号

`\#,\$,\%,\&,\_,\|`

$\#,\$,\%,\&,\_,\|$

## 公式上下层符号

|展示|代码|
|-|-|
|$\acute{123}$|`\acute{123}`|
|$\bar{123}$|`\bar{123}`|
|$\breve{123}$|`\breve{123}`|
|$\check{123}$|`\check{123}`|
|$\dot{123}$|`\dot{123}`|
|$\ddot{123}$|`\ddot{123}`|
|$\dddot{123}$|`\dddot{123}`|
|$\ddddot{123}$|`\ddddot{123}`|
|$\grave{123}$|`\grave{123}`|
|$\hat{123}$|`\hat{123}`|
|$\mathring{123}$|`\mathring{123}`|
|$\tilde{123}$|`\tilde{123}`|
|$\vec{123}$|`\vec{123}`|
|$\overleftarrow{123}$|`\overleftarrow{123}`|
|$\overrightarrow{123}$|`\overrightarrow{123}`|
|$\overleftrightarrow{123}$|`\overleftrightarrow{123}`|
|$\overline{123}$|`\overline{123}`|
|$\widehat{123}$|`\widehat{123}`|
|$\widetilde{123}$|`\widetilde{123}`|
|$\underline{123}$|`\underline{123}`|
|$\underset{123}{abc}$|`\underset{123}{abc}`|
|$\overset{123}{abc}$|`\overset{123}{abc}`|
|$\underbrace{123}_{abc}$|`\underbrace{123}_{abc}`|
|$\xleftarrow[123]{abc}$|`\xleftarrow[123]{abc}`|
|$\xrightarrow[123]{abc}$|`\xrightarrow[123]{abc}`|

## 箭头

|箭头|代码|
|-|-|
|$\uparrow,\downarrow,\leftarrow,\rightarrow$|`\uparrow,\downarrow,\leftarrow,\rightarrow`|
|$\Uparrow,\Downarrow,\Leftarrow,\Rightarrow$|`\Uparrow,\Downarrow,\Leftarrow,\Rightarrow`|
|$\upuparrows,\downdownarrows,\leftleftarrows,\rightrightarrows$|`\upuparrows,\downdownarrows,\leftleftarrows,\rightrightarrows`|
|$\nwarrow,\nearrow,\swarrow,\searrow$|`\nwarrow,\nearrow,\swarrow,\searrow`|
|$\upharpoonleft,\upharpoonright,\downharpoonleft,\downharpoonright$|`\upharpoonleft,\upharpoonright,\downharpoonleft,\downharpoonright`|
|$\leftharpoondown,\leftharpoonup,\rightharpoondown,\rightharpoonup$|`\leftharpoondown,\leftharpoonup,\rightharpoondown,\rightharpoonup`|
|$\longleftarrow,\longrightarrow,\longleftrightarrow$|`\longleftarrow,\longrightarrow,\longleftrightarrow`|
|$\Longleftarrow,\Longrightarrow,\Longleftrightarrow$|`\Longleftarrow,\Longrightarrow,\Longleftrightarrow`|
|$\nleftarrow,\nrightarrow,\nleftrightarrow$|`\nleftarrow,\nrightarrow,\nleftrightarrow`|
|$\nLeftarrow,\nRightarrow,\nLeftrightarrow$|`\nLeftarrow,\nRightarrow,\nLeftrightarrow`|
|$\leftrightarrow,\updownarrow$|`\leftrightarrow,\updownarrow`|
|$\Leftrightarrow,\Updownarrow$|`\Leftrightarrow,\Updownarrow`|
|$\twoheadleftarrow,\twoheadrightarrow$|`\twoheadleftarrow,\twoheadrightarrow`|
|$\hookleftarrow,\hookrightarrow$|`\hookleftarrow,\hookrightarrow`|
|$\Lleftarrow,\Rrightarrow$|`\Lleftarrow,\Rrightarrow`|
|$\Lsh,\Rsh$|`\Lsh,\Rsh`|
|$\dashleftarrow,\dashrightarrow$|`\dashleftarrow,\dashrightarrow`|
|$\looparrowleft,\looparrowright$|`\looparrowleft,\looparrowright`|
|$\leftarrowtail,\rightarrowtail$|`\leftarrowtail,\rightarrowtail`|
|$\circlearrowleft,\circlearrowright$|`\circlearrowleft,\circlearrowright`|
|$\curvearrowleft,\curvearrowright$|`\curvearrowleft,\curvearrowright`|
|$\leftrightarrows,\rightleftarrows$|`\leftrightarrows,\rightleftarrows`|
|$\rightleftharpoons,\leftrightharpoons$|`\rightleftharpoons,\leftrightharpoons`|
|$\longmapsto$|`\longmapsto`|
|$\mapsto$|`\mapsto`|
|$\leftrightsquigarrow,\rightsquigarrow$|`\leftrightsquigarrow,\rightsquigarrow`|

## 点和省略号

|展示|代码|
|-|-|
|$a\cdot b$|`\cdot b`|
|$a\cdotp b$|`\cdotp b`|
|$a\centerdot b$|`\centerdot b`|
|$\cdots$|`\cdots`|
|$\ddots$|`\ddots`|
|$\dots$|`\dots`|
|$\ldotp$|`\ldotp`|
|$\ldots$|`\ldots`|
|$\vdots$|`\vdots`|

## 函数

|展示|代码|||||
|-|-|-|-|-|-|
|$\sin$|`\sin`|$\cos$|`\cos`|$\tan$|`\tan`|
|$\cot$|`\cot`|$\csc$|`\csc`|$\sec$|`\sec`|
|$\arccos$|`\arccos`|$\arcsin$|`\arcsin`|$\arctan$|`\arctan`|
|$\sinh$|`\sinh`|$\cosh$|`\cosh`|$\tanh$|`\tanh`|
|$\coth$|`\coth`|$\exp$|`\exp`|$\log$|`\log`|
|$\lg$|`\lg`|$\ln$|`\ln`|$\max$|`\max`|
|$\min$|`\min`|$\gcd$|`\gcd`||

## 微积分与极限

|展示|代码|||||
|-|-|-|-|-|-|
|$\nabla$|`\nabla`|$\partial$|`\partial`|$\prime,'$|`\prime,'`|
|$\inf$|`\inf`|$\int,\iint,\iiint,\iiiint$|`\int,\iint,\iiint,\iiiint`|$\oint$|`\oint`|
|$\lim$|`\lim`|$\liminf$|`\liminf`|$\limsup$|`\limsup`|
|$\injlim$|`\injlim`|$\projlim$|`\projlim`|$\varinjlim$|`\varinjlim`|
|$\varlimsup$|`\varlimsup`|$\varliminf$|`\varliminf`|$\varprojlim$|`\varprojlim`|
|$\infty$|`\infty`|$\idotsint$|`\idotsint`|||

## 类字母符号

|展示|代码|
|-|-|
|$\Bbbk,\complement,\backepsilon,\Game,\digamma,\hbar,\hslash$|`\Bbbk,\complement,\backepsilon,\Game,\digamma,\hbar,\hslash`|
|$\Im,\imath,\jmath,\ell,\mho,\Re,\S,\top,\wp$|`\Im,\imath,\jmath,\ell,\mho,\Re,\S,\top,\wp`|

## 集合

|展示|代码|
|-|-|
|$\in,\notin,\ni,\owns$|`\in,\notin,\ni,\owns`|
|$\subset,\Subset,\subseteq,\subsetneq,\nsubseteq,\nsubseteqq$|`\subset,\Subset,\subseteq,\subsetneq,\nsubseteq,\nsubseteqq`|
|$\supset,\Supset,\supseteq,\supsetneq,\nsupseteq,\nsupseteqq$|`\supset,\Supset,\supseteq,\supsetneq,\nsupseteq,\nsupseteqq`|
|$\subseteqq,\subsetneqq,\varsubsetneq,\varsubsetneqq$|`\subseteqq,\subsetneqq,\varsubsetneq,\varsubsetneqq`|
|$\supseteqq,\supsetneqq,\varsupsetneq,\varsupsetneqq$|`\supseteqq,\supsetneqq,\varsupsetneq,\varsupsetneqq`|
|$\emptyset,\varnothing$|`\emptyset,\varnothing`|

## 关系运算符

|展示|代码|
|-|-|
|$>,\ge,\geqq,\geqslant,\gg,\ggg,\gt,\gtrdot,\eqslantgtr$|`>,\ge,\geqq,\geqslant,\gg,\ggg,\gt,\gtrdot,\eqslantgtr`|
|$<,\le,\leqq,\leqslant,\ll,\lll,\lt,\lessdot,\eqslantless$|`<,\le,\leqq,\leqslant,\ll,\lll,\lt,\lessdot,\eqslantless`|
|$\gtrapprox,\gnapprox,\gneq,\gneqq,\gvertneqq,\gtrsim,\gnsim$|`\gtrapprox,\gnapprox,\gneq,\gneqq,\gvertneqq,\gtrsim,\gnsim`|
|$\lessapprox,\lnapprox,\lneq,\lneqq,\lvertneqq,\lesssim,\lnsim$|`\lessapprox,\lnapprox,\lneq,\lneqq,\lvertneqq,\lesssim,\lnsim`|
|$\gtreqless,\gtreqqless,\gtrless,\lesseqgtr,\lesseqqgtr,\lessgtr$|`\gtreqless,\gtreqqless,\gtrless,\lesseqgtr,\lesseqqgtr,\lessgtr`|
|$\ngeq,\ngeqq,\ngeqslant,\ngtr,\nleq,\nleqq,\nleqslant,\nless$|`\ngeq,\ngeqq,\ngeqslant,\ngtr,\nleq,\nleqq,\nleqslant,\nless`|
|$\sqsubset,\sqsupset,\sqsubseteq,\sqsupseteq$|`\sqsubset,\sqsupset,\sqsubseteq,\sqsupseteq`|
|$\prec,\preccurlyeq,\curlyeqprec,\preceq,\precsim,\precapprox$|`\prec,\preccurlyeq,\curlyeqprec,\preceq,\precsim,\precapprox`|
|$\precnapprox,\precneqq,\precnsim,\nprec,\npreceq$|`\precnapprox,\precneqq,\precnsim,\nprec,\npreceq`|
|$\succ,\curlyeqsucc,\succcurlyeq,\succeq,\succsim,\succapprox$|`\succ,\curlyeqsucc,\succcurlyeq,\succeq,\succsim,\succapprox`|
|$\succnapprox,\succneqq,\succnsim,\nsucc,\nsucceq$|`\succnapprox,\succneqq,\succnsim,\nsucc,\nsucceq`|
|$\sim,\nsim,\thicksim,\backsim,\simeq,\backsimeq,\eqsim$|`\sim,\nsim,\thicksim,\backsim,\simeq,\backsimeq,\eqsim`|
|$\approx,\thickapprox,\approxeq$|`\approx,\thickapprox,\approxeq`|
|$\vdash,\dashv,\Vdash,\vDash,\Vvdash,\models$|`\vdash,\dashv,\Vdash,\vDash,\Vvdash,\models`|
|$\nvdash,\nVdash,\nVDash,\nvDash$|`\nvdash,\nVdash,\nVDash,\nvDash`|
|$\ntriangleleft,\ntriangleright$|`\ntriangleleft,\ntriangleright`|
|$\trianglelefteq,\trianglerighteq,\ntrianglelefteq,\ntrianglerighteq$|`\trianglelefteq,\trianglerighteq,\ntrianglelefteq,\ntrianglerighteq`|
|$=,\eqcirc,\equiv,\ne,\cong,\ncong$|`=,\eqcirc,\equiv,\ne,\cong,\ncong`|
|$\Doteq,\doteq,\triangleq$|`\Doteq,\doteq,\triangleq`|
|$\Bumpeq,\bumpeq,\circeq$|`\Bumpeq,\bumpeq,\circeq`|
|$\propto,\varpropto$|`\propto,\varpropto`|

## 算术与逻辑运算符

|展示|代码|
|-|-|
|$\circ,\bullet,\bigcirc$|`\circ,\bullet,\bigcirc`|
|$\cap,\Cap,\bigcap,\doublecap,\sqcap$|`\cap,\Cap,\bigcap,\doublecap,\sqcap`|
|$\cup,\Cup,\bigcup,\doublecup,\sqcup,\bigsqcup$|`\cup,\Cup,\bigcup,\doublecup,\sqcup,\bigsqcup`|
|$+,-,\pm,\mp,\dotplus,\uplus,\biguplus,\sum$|`+,-,\pm,\mp,\dotplus,\uplus,\biguplus,\sum`|
|$\ast,\times,\div,\divideontimes,\prod$|`\ast,\times,\div,\divideontimes,\prod`|
|$\boxplus,\boxminus,\boxtimes$|`\boxplus,\boxminus,\boxtimes`|
|$\odot,\bigodot,\ominus,\oplus,\bigoplus,\oslash,\otimes$|`\odot,\bigodot,\ominus,\oplus,\bigoplus,\oslash,\otimes`|
|$\sqrt{16}=\sqrt[3]{64}$|`\sqrt{16}=\sqrt[3]{64}`|
|$\lor,\vee,\bigvee,\veebar,\curlyvee$|`\lor,\vee,\bigvee,\veebar,\curlyvee`|
|$\land,\wedge,\barwedge,\bigwedge,\doublebarwedge,\curlywedge$|`\land,\wedge,\barwedge,\bigwedge,\doublebarwedge,\curlywedge`|
|$\lnot,\neg$|`\lnot,\neg`|
|$\because,\therefore$|`\because,\therefore`|
|$\forall,\exists,\nexists$|`\forall,\exists,\nexists`|

## 几何符号

部分几何符号可能归入了特殊符号中。

|展示|代码|
|-|-|
|$\angle,\measuredangle,\sphericalangle$|`\angle,\measuredangle,\sphericalangle`|
|$\perp,\bot$|`\perp,\bot`|
|$\mid,\nmid,\parallel,\nparallel$|`\mid,\nmid,\parallel,\nparallel`|
|$\shortmid,\shortparallel,\nshortmid,\nshortparallel$|`\shortmid,\shortparallel,\nshortmid,\nshortparallel`|

## 特殊符号

|展示|代码|
|-|-|
|$\bigtriangleup,\triangle,\vartriangle$|`\bigtriangleup,\triangle,\vartriangle`|
|$\bigtriangledown,\triangledown$|`\bigtriangledown,\triangledown`|
|$\triangleleft,\vartriangleleft,\lhd$|`\triangleleft,\vartriangleleft,\lhd`|
|$\triangleright,\vartriangleright,\rhd$|`\triangleright,\vartriangleright,\rhd`|
|$\bigstar,\blacklozenge,\blacksquare$|`\bigstar,\blacklozenge,\blacksquare`|
|$\blacktriangle,\blacktriangledown,\blacktriangleleft,\blacktriangleright$|`\blacktriangle,\blacktriangledown,\blacktriangleleft,\blacktriangleright`|
|$\Box,\square,\boxdot$|`\Box,\square,\boxdot`|
|$\circledast,\circledcirc,\circleddash,\circledR,\circledS$|`\circledast,\circledcirc,\circleddash,\circledR,\circledS`|
|$\dagger,\ddagger$|`\dagger,\ddagger`|
|$\diagdown,\diagup$|`\diagdown,\diagup`|
|$\diamond,\Diamond,\lozenge$|`\diamond,\Diamond,\lozenge`|
|$\heartsuit,\diamondsuit,\clubsuit,\spadesuit$|`\heartsuit,\diamondsuit,\clubsuit,\spadesuit`|
|$\flat,\natural,\sharp$|`\flat,\natural,\sharp`|
|$\checkmark,\surd$|`\checkmark,\surd`|
|$\smile,\frown,\asymp$|`\smile,\frown,\asymp`|
|$\ulcorner\urcorner$|`\ulcorner\urcorner`|
|$\llcorner\lrcorner$|`\llcorner\lrcorner`|
|$\lhd\rhd$|`\lhd\rhd`|
|$\LaTeX,\TeX$|`\LaTeX,\TeX`|
|$\Finv$|`\Finv`|
|$\maltese$|`\maltese`|
|$\backprime$|`\backprime`|
|$\between$|`\between`|
|$\multimap$|`\multimap`|
|$\pitchfork$|`\pitchfork`|
|$\star$|`\star`|
|$\yen$|`\yen`|
|$\intercal$|`\intercal`|
|$\wr$|`\wr`|
|$\backslash$|`\backslash`|

## 其它未分类符号

|展示|代码|
|-|-|
|$\leftthreetimes,\rightthreetimes$|`\leftthreetimes,\rightthreetimes`|
|$\coprod,\amalg$|`\coprod,\amalg`|
|$\sup$|`\sup`|
|$\arg$|`\arg`|
|$\deg$|`\deg`|
|$\dim$|`\dim`|
|$\hom$|`\hom`|
|$\ker$|`\ker`|
|$\Pr$|`\Pr`|
|$\det$|`\det`|
|$\ltimes\rtimes,\bowtie,\Join$|`\ltimes\rtimes,\bowtie,\Join`|

## 用`\DeclareMathOperator`定义运算符

```latex
$\DeclareMathOperator{\lcm}{lcm} \lcm(4,6)=2$
$\lcm(12,18)=24$
```

$\DeclareMathOperator{\lcm}{lcm} \lcm(4,6)=2$
$\lcm(12,18)=24$

## `\buildrel{} \over{}`

用于自创运算符，这个运算符拥有两行。

```latex
\buildrel{\rm def} \over{:=}
```

$$\buildrel{\rm def} \over{:=}$$

## `\substack`

用于编写大型运算符的条件时分行。

```latex
\sum_{\substack{1\lt i\lt 3 \\1\le j\lt 5}}a_{ij}
```

$$\sum_{\substack{1\lt i\lt 3 \\1\le j\lt 5}}a_{ij}$$

## `\begin{} ... \end{}`

### `aligned`

```latex
\begin{aligned}
3x - 4y &= 5 \\
x + 7 &= -2y
\end{aligned}
\tag{3.1c}
```

$$\begin{aligned}
3x - 4y &= 5 \\
x + 7 &= -2y
\end{aligned}
\tag{3.1c}$$

### `align`

```latex
\begin{align}
(a+b)^2 &= (a+b)(a+b)          \tag{1}  \\
        &= a^2 + ab + ba + b^2 \tag{2}  \\
        &= a^2 + 2ab + b^2     \tag{3}
\end{align}
```

$$\begin{align}
(a+b)^2 &= (a+b)(a+b)          \tag{1}  \\
        &= a^2 + ab + ba + b^2 \tag{2}  \\
        &= a^2 + 2ab + b^2     \tag{3}
\end{align}$$

### `array`

l,c,r分别表示当前一列是居左，居中，还是居右。如果有|，那么就代表隔开。

```latex
\begin{array}{lc|r}
aaa & bbb & ccc\\
d & e & f
\end{array}
```

$$\begin{array}{l|c|r}
aaa & bbb & ccc\\
d & e & f
\end{array}$$

### `cases`

```latex
|x| =
\begin{cases}
x  & \text{ if } x\ge 0 \\
-x & \text{ if } x \lt 0
\end{cases}$$
```

$$|x| =
\begin{cases}
x  & \text{ if } x\ge 0 \\
-x & \text{ if } x \lt 0
\end{cases}$$

### `Bmatrix`

```latex
\begin{Bmatrix} a & b\\ c & d\end{Bmatrix}
```

$$\begin{Bmatrix} a & b\\ c & d\end{Bmatrix}$$

### `bmatrix`

```latex
\begin{bmatrix} a & b\\ c & d\end{bmatrix}
```

$$\begin{bmatrix} a & b\\ c & d\end{bmatrix}$$

### `matrix`

```latex
\begin{matrix} a & b\\ c & d\end{matrix}
```

$$\begin{matrix} a & b\\ c & d\end{matrix}$$

### `pmatrix`

```latex
\begin{pmatrix} a & b\\ c & d\end{pmatrix}
```

$$\begin{pmatrix} a & b\\ c & d\end{pmatrix}$$

### `vmatrix`

```latex
\begin{vmatrix} a & b\\ c & d\end{vmatrix}
```

$$\begin{vmatrix} a & b\\ c & d\end{vmatrix}$$

### `Vmatrix`

```latex
\begin{Vmatrix} a & b\\ c & d\end{Vmatrix}
```

$$\begin{Vmatrix} a & b\\ c & d\end{Vmatrix}$$

### `eqnarray`

```latex
\begin{eqnarray}
(x-1)^2 &=& (x-1)(x-1)      &=&  x^2-2x + 1 \\
(x-1)^3 &=& (x-1)(x-1)(x-1) &=&  (x-1)^2(x-1) 
\end{eqnarray}
```

$$\begin{eqnarray}
(x-1)^2 &=& (x-1)(x-1)      &=&  x^2-2x + 1 \\
(x-1)^3 &=& (x-1)(x-1)(x-1) &=&  (x-1)^2(x-1)
\end{eqnarray}$$

### 其它

#### `\tag`

注意`\tag`只有某些情况下才可以使用，如`\aligned`不可以，`\align`可以。

```latex
\begin{align}
(a+b)^2 &= (a+b)(a+b)          \tag{1}  \\
        &= a^2 + ab + ba + b^2 \tag{2}  \\
        &= a^2 + 2ab + b^2     \tag{3}
\end{align}
```

$$\begin{align}
(a+b)^2 &= (a+b)(a+b)          \tag{1}  \\
        &= a^2 + ab + ba + b^2 \tag{2}  \\
        &= a^2 + 2ab + b^2     \tag{3}
\end{align}$$

#### `\hline, \hdashline`

用于在矩阵中画横线，`\hline`前者为实线，`\hdashline`为虚线。

```latex
\hline
x_{11} & x_{12} \\
x_{21} & x_{22} \\
\hdashline
x_{31} & x_{32} 
\end{matrix}
```

$$\begin{matrix}
\hline
x_{11} & x_{12} \\
x_{21} & x_{22} \\
\hdashline
x_{31} & x_{32}
\end{matrix}$$

## `\left`, `\right`和`\big`

根据括号内的公式高度，智能调整两侧括号的高度，一个`\left`必须和一个`\right`匹配。如果只想要其中一个，那么用`\right.`来代替。

|展示|代码|
|-|-|
|$\left(1+2\right)=\left(\dfrac{1}{2}\right)$|`\left(1+2\right)=\left(\dfrac{1}{2}\right)`|
|$\left\lgroup 1+2\right\rgroup=\left\lgroup\dfrac{1}{2}\right\rgroup$|`\left\lgroup 1+2\right\rgroup=\left\lgroup\dfrac{1}{2}\right\rgroup`|
|$\left[1+2\right]=\left[\dfrac{1}{2}\right]$|`\left[1+2\right]=\left[\dfrac{1}{2}\right]`|
|$\left\{1+2\right\}=\left\{\dfrac{1}{2}\right\}$|`\left\{1+2\right\}=\left\{\dfrac{1}{2}\right\}`|
|$\left\uparrow 1+2\right\downarrow=\left\downarrow\dfrac{1}{2}\right\uparrow$|`\left\uparrow 1+2\right\downarrow=\left\downarrow\dfrac{1}{2}\right\uparrow`|
|$\left\Uparrow 1+2\right\Downarrow=\left\Downarrow\dfrac{1}{2}\right\Uparrow$|`\left\Uparrow 1+2\right\Downarrow=\left\Downarrow\dfrac{1}{2}\right\Uparrow`|
|$\left\updownarrow 1+2\right\Updownarrow=\left\Updownarrow\dfrac{1}{2}\right\updownarrow$|`\left\updownarrow 1+2\right\Updownarrow=\left\Updownarrow\dfrac{1}{2}\right\updownarrow`|
|$\left\vert 1+2\right\vert=\left\vert\dfrac{1}{2}\right\vert$|`\left\vert 1+2\right\vert=\left\vert\dfrac{1}{2}\right\vert`|
|$\left\Vert 1+2\right\Vert=\left\Vert\dfrac{1}{2}\right\Vert$|`\left\Vert 1+2\right\Vert=\left\Vert\dfrac{1}{2}\right\Vert`|
|$\left\bracevert 1+2\right\bracevert=\left\bracevert\dfrac{1}{2}\right\bracevert$|`\left\bracevert 1+2\right\bracevert=\left\bracevert\dfrac{1}{2}\right\bracevert`|
|$\left\lceil 1+2\right\rceil=\left\lceil\dfrac{1}{2}\right\rceil$|`\left\lceil 1+2\right\rceil=\left\lceil\dfrac{1}{2}\right\rceil`|
|$\left\lfloor 1+2\right\rfloor=\left\lfloor\dfrac{1}{2}\right\rfloor$|`\left\lfloor 1+2\right\rfloor=\left\lfloor\dfrac{1}{2}\right\rfloor`|
|$\left/ 1+2\right\backslash=\left/\dfrac{1}{2}\right\backslash$|`\left/ 1+2\right\backslash=\left/\dfrac{1}{2}\right\backslash`|
|$\left\lmoustache 1+2\right\rmoustache=\left\lmoustache\dfrac{1}{2}\right\rmoustache$|`\left\lmoustache 1+2\right\rmoustache=\left\lmoustache\dfrac{1}{2}\right\rmoustache`|

也可以自行直接指定大小：

```latex
\Bigg[\bigg[\Big[\big[ [
```

$$\Bigg[\bigg[\Big[\big[ [$$

### `\not`

在任何一个关系运算符前面添加一个`\not`，即可得到划斜线的运算符，如：

|展示|代码|
|-|-|
|$\not\equiv$|`\not\equiv`|
|$\not=$|`\not=`|
|$\not\in$|`\not\in`|
