---
title: Project Euler 336
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-08 17:06:08
---

<escape><!-- more --></escape>

# Project Euler 336

## 题目

### Maximix Arrangements

A train is used to transport four carriages in the order: ABCD. However, sometimes when the train arrives to collect the carriages they are not in the correct order.

To rearrange the carriages they are all shunted on to a large rotating turntable. After the carriages are uncoupled at a specific point the train moves off the turntable pulling the carriages still attached with it. The remaining carriages are rotated $180$ degrees. All of the carriages are then rejoined and this process is repeated as often as necessary in order to obtain the least number of uses of the turntable.

Some arrangements, such as ADCB, can be solved easily: the carriages are separated between A and D, and after DCB are rotated the correct order has been achieved.

However, Simple Simon, the train driver, is not known for his efficiency, so he always solves the problem by initially getting carriage A in the correct place, then carriage B, and so on.

Using four carriages, the worst possible arrangements for Simon, which we shall call *maximix arrangements*, are DACB and DBAC; each requiring him five rotations (although, using the most efficient approach, they could be solved using just three rotations). The process he uses for DACB is shown below.

![](../images/p336_maximix.gif)

It can be verified that there are $24$ maximix arrangements for six carriages, of which the tenth lexicographic maximix arrangement is DFAECB.

Find the $2011^{\text{th}}$ lexicographic maximix arrangement for eleven carriages.

## 解决方案

令$N=11,Q=2011$。

可以知道，最大的安排数是$2N-3$。这里使用数字$1$代表车厢A，$2$代表B，$3$代表C……按照这个人的排序方式，当$1$不在第$1$个位置并且不在第$N$个位置，那么他就需要$2$次翻转。翻转完成后，若$2$不在不在第$2$个位置并且不在第$N$个位置，那么同样需要$2$次翻转……最终到了第$N-1$个车厢，只有它在第$N$个位置时才翻转，而第$N$个车厢已经排好序。因此最大安排数为$2N-3$。

因此，直接暴力枚举每个排列，按照题中的算法进行排序，直到找到第$Q$个排列。

为了减少枚举量，发现第一个位置不可能为$1$或者是$2$。因为第一个是$1$，那就直接被算法跳过，肯定不是最优的；如果第一个是$2$，那么当$1$被翻转到第一个位置时，$2$将会在序列末尾，而不会在中间，少了所要求的一次翻转次数。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
const int N=11,Q=2011;
int a[N],b[N];
int main(){
    a[0]=2;a[1]=0;a[2]=1;
    for(int i=3;i<N;i++)
        a[i]=i;
    int v=2*N-3,cnt=0;
    do{
        int c=0;
        memcpy(b,a,sizeof(a));
        for(int i=0,p=0;i<N;i++){
            if(b[i]==i) break;
            if(b[N-1]!=i){
                for(p=i+1;b[p]!=i;p++);
                reverse(b+p,b+N);
                ++c;
            }
            reverse(b+i,b+N);
            ++c;
        }
        if(c==v&&++cnt==Q) break;
    }while(next_permutation(a,a+N));
    string ans="";
    for(int i=0;i<N;i++)
        ans+='A'+a[i];
    cout<<ans<<endl;
}

```
