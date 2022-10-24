---
title: Project Euler 170
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-19 21:56:50
---

<escape><!-- more --></escape>

# Project Euler 170

## 题目

### Find the largest 0 to 9 pandigital that can be formed by concatenating products

Take the number $6$ and multiply it by each of $1273$ and $9854$:

$6 × 1273 =  7638$<br>
$6 × 9854 = 59124$

By concatenating these products we get the $1$ to $9$ pandigital $763859124$. We will call $763859124$ the “concatenated product of $6$ and $(1273,9854)$”. Notice too, that the concatenation of the input numbers, $612739854$, is also $1$ to $9$ pandigital.

The same can be done for $0$ to $9$ pandigital numbers.

What is the largest $0$ to $9$ pandigital $10$-digit concatenated product of an integer with two or more other integers, such that the concatenation of the input numbers is also a $0$ to $9$ pandigital 10-digit number?

## 解决方案

假设算式的形式为$a(a_0,a_1,\dots)=(b_0,b_1,\dots)$。

通过枚举搜索答案：

1. 从大到小遍历候选的全排列，如果判定正确就退出。
2. 将整个全$0\sim 9$数串划分成多个子串，然后求最大公因数$\gcd(b_0,b_1,\dots)$。最大公因数的因子为乘数$a$的一个候选答案。因此，在计算开始之前现将$10^5$以内的所有数的因子保存（$1$除外）。
3. 为保证搜索效率，可以假设括号$()$中只有两个数$a_0,a_1$，这不影响寻找正确答案。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N=100004;
int a[14];
vector<int>d[N];
string tp="0123456789";
bool ok(){
    for(int p=1;p<10;p++){
        if(a[p]==0) continue;
        int l=0,r=0;
        for(int i=0;i<10;i++) {
            if (i < p) l = l * 10 + a[i];
            else r = r * 10 + a[i];
        }
        for(int x:d[__gcd(l,r)]) {
            string s = to_string(x) + to_string(l / x) + to_string(r / x);
            sort(s.begin(), s.end());
            if (s == tp) {
                return true;
            }
        }
    }
    return false;
}
int main(){
    for(int i=3;i<N;i+=3){
        for(int j=i;j<N;j+=i)
            d[j].push_back(i);
    }
    for(int i=0;i<10;i++)
        a[i]=9-i;
    do{
        if (ok()) break;
    } while (prev_permutation(a,a+10));
    string ans;
    for(int i=0;i<10;i++)
        ans+=char('0'+a[i]);
    cout<<ans<<endl;
}
```
