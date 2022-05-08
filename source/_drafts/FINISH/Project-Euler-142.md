---
title: Project Euler 142
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 142
## 题目
### Perfect Square Collection
Find the smallest $x + y + z$ with integers $x > y > z > 0$ such that $x + y, x - y, x + z, x - z, y + z, y - z$ are all perfect squares.


## 解决方案

令这六个数分别为六个平方数
$\begin{aligned}
&x+y=a^2\\
&x-y=b^2\\
&x+z=c^2\\
&x-z=d^2\\
&y+z=e^2\\
&y-z=f^2
\end{aligned}$

将其中的一些式子相减，代入，可以得到以下式子：

$\begin{aligned}
&e^2=a^2-d^2\\
&f^2=a^2-c^2\\
&b^2=c^2-e^2\\
\end{aligned}$

我们最终枚举$a,c,e$三个值寻找答案，另外不难发现$a>c>e$。

由于本题的每个平方数的上限难以确定，故拟定为$10^6$。

另外，在枚举过程中，需要保证$a>b,c>d,e>f$。以及最终算出来的$x,y,z$必须是个正整数。

## 代码


```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 1000000;
int solve(){
    unordered_set<int>st;
    for(int i=1;i*i<=N;i++)
        st.insert(i*i);
    for(int a=1,a2;(a2=a*a)<=N;a++){
        for(int c=1;c<a;c++){
            int c2=c*c;
            int f2=a2-c2;
            if(!st.count(f2)) continue;
            for(int e=1;e<c;e++){
                int e2=e*e;
                int b2=c*c-e*e;
                if(!st.count(b2)) continue;
                int d2=a2-e2;
                if(st.count(d2)){
                    if(a2>b2&&c2>d2&&e2>f2&&(a2+b2)%2==0&&(e2+f2)%2==0){
                        return (a2+c2+e2)>>1;
                    }
                }
            }
        }
    }
    return -1;
}
int main(){
    printf("%d\n",solve());
}

```