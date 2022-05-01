---
title: Project Euler 87
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 87
## 题目
### Prime power triples
The smallest number expressible as the sum of a prime square, prime cube, and prime fourth power is $28$. In fact, there are exactly four numbers below fifty that can be expressed in such a way:

$28 = 2^2 + 2^3 + 2^4$
$33 = 3^2 + 2^3 + 2^4$
$49 = 5^2 + 2^3 + 2^4$
$47 = 2^2 + 3^3 + 2^4$

How many numbers below fifty million can be expressed as the sum of a prime square, prime cube, and prime fourth power?

### 解决方案

令$N=5\times10^7$。

观察到，这里的和都是质数的$2$次方及以上。因此，可以先预处理所有$\sqrt N$以内的质数，再将这些质数的$2,3,4$次方按序存放在数组a2, a3, a4中。

直接枚举$3$个列表中每个组合，再将$3$个数的和存放进集合即可。

## 代码
```py
from tools import get_prime, int_sqrt

N = 5 * 10 ** 7
M = int_sqrt(N)
pr = get_prime(M)
a2 = [x * x for x in pr]
a3 = [x ** 3 for x in pr if x ** 3 <= N]
a4 = [x ** 4 for x in pr if x ** 4 <= N]
st = set()
for x in a2:
    for y in a3:
        if x + y >= N:
            break
        for z in a4:
            if x + y + z >= N:
                break
            st.add(x + y + z)
ans = len(st)
print(ans)

```