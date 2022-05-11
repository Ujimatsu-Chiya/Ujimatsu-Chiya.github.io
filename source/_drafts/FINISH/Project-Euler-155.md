---
title: Project Euler 155
tags:
  - Project Euler
  - OEIS
mathjax: true
---
<escape><!-- more --></escape>


# Project Euler 155
## 题目
### Counting Capacitor Circuits
An electric circuit uses exclusively identical capacitors of the same value $C$.

The capacitors can be connected in series or in parallel to form sub-units, which can then be connected in series or in parallel with other capacitors or other sub-units to form larger sub-units, and so on up to a final circuit.

Using this simple procedure and up to n identical capacitors, we can make circuits having a range of different total capacitances. For example, using up to $n=3$ capacitors of $60\mu F$ each, we can obtain the following $7$ distinct total capacitance values: 

![](../images/p155_capacitors1.gif)

If we denote by $D(n)$ the number of distinct total capacitance values we can obtain when using up to n equal-valued capacitors and the simple procedure described above, we have: $D(1)=1, D(2)=3, D(3)=7 \dots$

Find $D(18)$.

*Reminder :*  When connecting capacitors $C_1, C_2$ etc in parallel, the total capacitance is $C_T=C_1+C_2+\dots$, whereas when connecting them in series, the overall capacitance is given by:$\dfrac{1}{C_T}=\dfrac{1}{C_1}+\dfrac{1}{C_2}+\dots$.


## 解决方案

目前的办法应该只有暴力枚举，剩下的只是优化：

1. 为减少枚举量，如果全局集合已经有的值，那就不需要继续添加到当前集合了。
2. 实现一个简易的分数类，避免用浮点数产生误差，同时避免进行除法操作。

枚举的思想：如果已经有一对整体的电容值分别是$u,v$，那么分别把这两“块”进行串联或者并联，得到新值$\dfrac{1}{\dfrac{1}{u}+\dfrac{1}{v}},u+v$。

这个数列在OEIS上的查询结果为[A153588](https://oeis.org/A153588)。
## 代码


```C++
# include <bits/stdc++.h>

using namespace std;
typedef long long ll;
const int N = 18;
struct Fraction{
    ll numerator,denominator;
    Fraction operator + (Fraction f){
        ll num = numerator*f.denominator+denominator*f.numerator;
        ll den = denominator*f.denominator;
        ll g=__gcd(num,den);
        return {num/g,den/g};
    }
    Fraction inv(){
        return {denominator,numerator};
    }
    //这里的小于只是为了用于区分分数的不同，而并非是分数的值大小本身。
    bool operator < (const Fraction &f) const{
        return numerator<f.numerator||numerator==f.numerator&&denominator<f.denominator;
    }
};
set<Fraction>st,now[N+2];
int main(){
    st.insert(Fraction{1,1});
    now[1].insert(Fraction{1,1});
    for(int i=2;i<=N;i++){
        for(int j=1;j<=i/2;j++){
            for(Fraction u:now[j]){
                for(Fraction v:now[i-j]){
                    Fraction x=u+v,y=(u.inv()+v.inv()).inv();
                    if(!st.count(x)){
                        st.insert(x);
                        now[i].insert(x);
                    }
                    if(!st.count(y)){
                        st.insert(y);
                        now[i].insert(y);
                    }
                }
            }
        }
    }
    int ans=st.size();
    printf("%d\n",ans);

}

```