---
title: Project Euler 571
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 571
## 题目
### Super Pandigital Numbers


A positive number is **pandigital** in base $b$ if it contains all digits from $0$ to $b - 1$ at least once when written in base $b$.

A *$n$-super-pandigital* number is a number that is simultaneously pandigital in all bases from $2$ to $n$ inclusively.

For example $978 = 1111010010_2 = 1100020_3 = 33102_4 = 12403_5$ is the smallest $5$-super-pandigital number.

Similarly, $1093265784$ is the smallest $10$-super-pandigital number.

The sum of the $10$ smallest $10$-super-pandigital numbers is $20319792309$.

What is the sum of the $10$ smallest $12$-super-pandigital numbers?



## 解决方案

令$N=12$。本题通过按照字典序大小暴力枚举$N$阶置换。然后再从$11$到$4$进制判断这个数是否符合条件（不需要判断$2,3$进制，因为这个数只要符合$9$进制，那么它一定符合$3$进制；任何一个二进制数都有$0,1$两位）。将符合条件的数相加即可。

## 代码

本份代码效率略低，约$70s$。

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N=12;
int Q=10;
char a[N];
bool check(ll x,int b){
    int st=0,c=0;
    for(;x;x/=b){
        int w=x%b;
        if(!(st>>w&1)&&++c==b) return 1;
        st|=1<<w;
    }
    return 0;
}
int main(){
    a[0]=1;a[1]=0;
    for(int i=2;i<N;i++)
        a[i]=i;
    ll ans=0;
    do{
        ll x=0;
        for(int i=0;i<N;i++)
            x=x*N+a[i];
        bool ok=1;
        for(int i=N-1;i>3&&ok;i--)
            if(!check(x,i)) ok=0;
        if(ok){
            vector<int>a;
            ans+=x;
            for(;x;x/=(N-1)){
                a.push_back(x%(N-1));
            }
            reverse(a.begin(),a.end());
            if(--Q==0) break;
        }
    }while(next_permutation(a,a+N));
    printf("%lld\n",ans);
}

```

