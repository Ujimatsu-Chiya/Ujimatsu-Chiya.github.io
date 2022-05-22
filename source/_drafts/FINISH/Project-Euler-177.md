---
title: Project Euler 177
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
    
# Project Euler 177
## 题目
### Integer angled Quadrilaterals

Let ABCD be a convex quadrilateral, with diagonals AC and BD. At each vertex the diagonal makes an angle with each of the two sides, creating eight corner angles.

![](../images/p177_quad.gif)

For example, at vertex $A$, the two angles are $CAD, CAB$.

We call such a quadrilateral for which all eight corner angles have integer values when measured in degrees an “integer angled quadrilateral”. An example of an integer angled quadrilateral is a square, where all eight corner angles are $45°$. Another example is given by $DAC = 20°, BAC = 60°, ABD = 50°, CBD = 30°, BCA = 40°, DCA = 30°, CDB = 80°, ADB = 50°$.

What is the total number of non-similar integer angled quadrilaterals?

Note: In your calculations you may assume that a calculated angle is integral if it is within a tolerance of $10^{-9}$ of an integer value.


## 解决方案

本题在枚举的过程中需要注意旋转、翻转的情况，需要去重。需要通过一些手段尽量减少枚举量。

只需要枚举其中四个角$DAC,BAC,ABD,CBD$的大小，就可以通过[正弦定理](https://mathworld.wolfram.com/LawofSines.html)和[余弦定理](https://mathworld.wolfram.com/LawofCosines.html)确定另外$4$个角的值，然后判断这些角是否都为整数。

具体过程见代码。

加上旋转，翻转后有八种方案，我们只保留其中一种。

## 代码

本代码根据题目下Thread的一份代码进行优化修改。

```C++
#include <bits/stdc++.h>
using namespace std;

double pi = acos(-1.0);
double sina[184];
double cosa[184];
unsigned hs(int a, int b, int c, int d) {
    return (a << 24) | (b << 16) | (c << 8) | d;
}

int main() {
    int ans = 0;
    for (int i = 0; i <= 180; i++) {
        sina[i] = sin(i * pi / 180);
        cosa[i] = cos(i * pi / 180);
    }
    // 不失一般性，枚举的角DAC是八个角中最小的。后续计算中如果发现有比这更小的角，则直接跳出循环。
    for (int DAC = 1; DAC <= 45; DAC++)
        // AB边上的另外两个角ABD，CBD至少有DAC这么大。
        for (int BAC = DAC; BAC <= 180 - DAC * 3; BAC++)
            // CBD至少有DAC这么大。
            for (int ABD = DAC; ABD <= 180 - 2 * DAC - BAC; ABD++)
                for (int CBD = DAC; CBD <= 180 - DAC - BAC - ABD; CBD++) {
                    int BCA = 180 - (BAC + ABD + CBD);
                    int ADB = 180 - (DAC + BAC + ABD);
                    // AB=1
                    double AC = sina[ABD + CBD] / sina[BCA];
                    double AD = sina[ABD] / sina[ADB];
                    double DC = sqrt(AC * AC + AD * AD - 2 * AC * AD * cosa[DAC]);
                    double tmpACD = acos((AC * AC + DC * DC - AD * AD) / (2 * AC * DC)) * 180 / pi;
                    int ACD = int(round(tmpACD));
                    if (fabs(tmpACD - ACD) > 1e-9) continue;
                    if (ACD < DAC) break;
                    int CDB = 180 - (DAC + ACD + ADB);
                    if (CDB < DAC) break;
                    unsigned h = hs(DAC, BAC, ABD, CBD);
                    if (h > hs(ABD, CBD, BCA, ACD)) continue;
                    if (h > hs(BCA, ACD, CDB, ADB)) continue;
                    if (h > hs(CDB, ADB, DAC, BAC)) continue;
                    if (h > hs(BAC, DAC, ADB, CDB)) continue;
                    if (h > hs(CBD, ABD, BAC, DAC)) continue;
                    if (h > hs(ACD, BCA, CBD, ABD)) continue;
                    if (h > hs(ADB, CDB, ACD, BCA)) continue;
                    ++ans;
                }
    printf("%d\n", ans);
    return 0;
}

```