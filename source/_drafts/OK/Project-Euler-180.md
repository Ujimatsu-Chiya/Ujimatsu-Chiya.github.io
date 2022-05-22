---
title: Project Euler 180
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 180
## 题目
### Rational zeros of a function of three variables

For any integer $n$, consider the three functions

$$f_{1,n}(x,y,z)=x^{n+1}+y^{n+1}-z^{n+1}$$
$$f_{2,n}(x,y,z)=(xy+yz+zx)(x^{n-1}+y^{n-1}-z^{n-1})$$
$$f_{3,n}(x,y,z)=xyz(x^{n-2}+y^{n-2}-z^{n-2})$$

and their combination

$$f_n(x,y,z)=f_{1,n}(x,y,z)+f_{2,n}(x,y,z)-f_{3,n}(x,y,z)$$

We call $(x,y,z)$ a golden triple of order $k$ if $x$, $y$, and $z$ are all rational numbers of the form $\dfrac{a}{b}$ with $0 <a < b \le k$ and there is (at least) one integer $n$, so that $f_n(x,y,z) = 0$.

Let $s(x,y,z) = x + y + z$.

Let $t = \dfrac{u}{v}$ be the sum of all distinct $s(x,y,z)$ for all golden triples $(x,y,z)$ of order $35$.

All the $s(x,y,z)$ and $t$ must be in reduced form.

Find $u + v$.


## 解决方案

经过整理，可以发现$f_n(x,y,z)=(x+y+z)(x^n+y^n-z^n)$

此时则变为求方程$x^n+y^n=z^n$是否有有理数解。


设$x=\dfrac{a}{b},y=\dfrac{c}{d},z=\dfrac{e}{f}$.

代入式子后，两边同乘$(bdf)^n$，即可化成$(adf)^n+(bcf)^n=(bde)^n$。

根据费马大定理，当$n\ge3$时无正整数解（题目中要求$n\le-3$时的情况也类似），故此时方程$x^n+y^n=z^n$没有有理数解。因此，本题只需求解$n=-2,-1,1,2$的情况即可。

不考虑$n=0$的情况，因为$f_0(x,y,z)=x+y+z>0$。
## 代码


```C++
# include <bits/stdc++.h>
using namespace std;
const int N = 35;
typedef long long ll;
struct Fraction {
    ll num, den;
    Fraction() {}
    Fraction(ll x, ll y = 1) {
        ll g = __gcd(x, y);
        num = x / g;
        den = y / g;
        if (den < 0) num = -num, den = -den;
    }
    Fraction rev() {
        return {den, num};
    }
    Fraction operator+(Fraction f) const {
        return {num * f.den + f.num * den, den * f.den};
    }
    Fraction operator*(Fraction f) const {
        return {num * f.num, den * f.den};
    }
    Fraction operator/(Fraction f) const {
        return {num * f.den, den * f.num};
    }
    bool operator<(Fraction f) const {
        return num * f.den < den * f.num;
    }
};
set<Fraction>st;
map<Fraction,Fraction>sq;
int main() {
    for (int b = 1; b <= N; b++) {
        for (int a = 1; a < b; a++) {
            if (__gcd(a, b) == 1) {
                st.insert(Fraction(a, b));
                sq[Fraction(a * a, b * b)] = Fraction(a, b);
            }
        }
    }
    set<Fraction> ans;
    vector<Fraction> v(st.begin(), st.end());
    for (int i = 0; i < v.size(); i++) {
        for (int j = i; j < v.size(); j++) {
            Fraction &x = v[i], &y = v[j];
            Fraction a = x + y;
            if (st.count(a)) ans.insert(a + x + y);
            a = (x * y) / (x + y);
            if (st.count(   a)) ans.insert(a + x + y);
            Fraction a2 = x * x + y * y;
            if (sq.count(a2))
                ans.insert(sq[a2] + x + y);
            a2 = (x * x * y * y) / (x * x + y * y);
            if (sq.count(a2))
                ans.insert(sq[a2] + x + y);
        }
    }
    Fraction f(1);
    for (Fraction w: ans) {
        f = f + w;
        printf("%lld/%lld\n",w.num,w.den);
    }
    printf("%lld %lld\n", f.num, f.den);
}
```