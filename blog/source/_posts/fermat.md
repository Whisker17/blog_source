---
title: 费马小定理
top: false
cover: false
toc: true
mathjax: true
date: 2020-10-10 16:15:59
password:
summary:
tags:
categories: Math | Cryptography
---











## 定理描述

假设 P 是一个素数，a 是一个整数，那么 $$a^P-a\ 是 P 的倍数$$ ，即 $$a^{p} ≡ a（mod\ p）$$ 

如果 a 不是 P 的倍数，这个定理也可以写成： $$a^{p-1} ≡ 1（mod\ p）$$

## 证明过程

根据同余的性质，只需要证明 $$a^P ≡ a \ (mod\ P)\ ，对于 0\le a \le P-1 成立，就可以可出上述定理。$$ 

反证法。假如结论不成立的话，就会有 i, j 两个数字，使得

![[公式]](https://www.zhihu.com/equation?tex=i+%2A+a+%5Cequiv+j+%2A+a%5Cpmod+n)

不妨假设 i > j，将上式移动一下位置，就会有

![[公式]](https://www.zhihu.com/equation?tex=%28i+-+j%29+%2A+a+%5Cequiv+0%5Cpmod+n)

换句话说，就是 (i - j) * a 可以被 n 整除。而 n 是素数，那么 (i - j) 或者 a 其中之一就必须包含因子 n。但 (i - j) 和 a 都比 n 要小，显然不可能包含因子 n。于是结论得证。

上面的证明中，不一定需要 a < n。只要 n 为素数，而 a, n 两者互质，证明也可成立，费马小定理也可成立。

\--------------------

因为乘以 a 再 mod n，只是 1 到 n - 1 的重新排列，数字并不会重复。于是我们就可以知道

![[公式]](https://www.zhihu.com/equation?tex=%281+%2A+2+%2A+3+....+n+-+1%29+%3D+%28a%5Cbmod+n%29%282a%5Cbmod+n%29%283a%5Cbmod+n%29+...+%28%28n-1%29a%5Cbmod+n%29)

应用同余的乘法原理，使用同余的记号，可以将上式记为

![[公式]](https://www.zhihu.com/equation?tex=%281+%2A+2+%2A+3+....+n+-+1%29+%5Cequiv+a+%2A+2a+%2A+3a+%2A+...+%28n-1%29a%5Cpmod+n)

将上式同时除以 ![[公式]](https://www.zhihu.com/equation?tex=%281+%2A+2+%2A+3+....+n+-+1%29) ，费马小定理得证

![[公式]](https://www.zhihu.com/equation?tex=a%5E%7Bn-1%7D%5Cequiv+1%5Cmod+n)