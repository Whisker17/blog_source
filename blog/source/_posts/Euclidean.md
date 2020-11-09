---
title: 欧几里得算法
top: false
cover: false
toc: true
mathjax: true
date: 2020-10-09 14:58:38
password:
summary:
tags:
categories: Math | Cryptography
---













## 欧几里得算法

又称**辗转相除法**，指的是：对于任意的非负整数 𝑎 和正整数 𝑏 ，求这两个数的**最大公因数** ，记为 $$gcd(a,b)$$ ，其中 gcd 是 greatest common division 的首字母组合。

辗转相除法基于如下原理：两个整数的最大公约数等于其中较小的数和两数相除余数的最大公约数，即 $$gcd(a,b) = gcd(b,a\ mod\ b)$$ 

### 证明过程

对于**任何**可以整除 a 和 b 的整数，那么它也一定能整除 a-b （和 b )，因此我们选择该整数（前面提到的**任何**整数）为 gcd(a,b) ，它一定比 a-b 和 b 的最大公约数小：$$gcd(a,b) \le gcd(a-b,b)$$ 

同理，任何可以整除 a-b 和 b 的整数，一定可以整除 a 和 b ，因此我们选择该整数为 gcd(a-b,b) ，它一定比 a 和 b 的最大公约数小：$$gcd(a-b,b)\le gcd(a,b)$$

由此可得： $$gcd(a,b)=gcd(a-b,b)$$

必然存在整数 n ，使得 $$a - n*b = a \ mod\  b$$，所以迭代可知：

$$gcd(a-b,b)=gcd(a-2b,b)=...=gcd(a-n*b,b)=gcd(a \ mod\  b,b)$$

### 实现及其工程优化

```python
def gcd(num1,num2):
    while num1 % num2 != 0:
        num1, num2 = num2, num1
    if num1 % num2 == 0:
        return num2
```

但是当整数很大时，取模运算的性能较低，所以我们对其进行优化，使用 **移位运算 + 更相减损术**

```python
def gcd(num1,num2):
	if num1 < num2:
        return gcd(num2,num1)
    if num1 == num2:
        return num2
    if (num1 % num2 == 0) and (num2 % 2 == 0):
        return gcd(num1 >> 1, num2 >> 1) << 1
    elif (num1 % 2 == 0):
        return gcd(num1 >> 1, num2)
    elif (num2 % 2 == 0):
        return gcd(num1, num2 >> 1)
    else:
        return gcd(num2, num1-num2)
```

## 扩展欧几里得算法

是欧几里得算法的扩展。已知整数 a，b，扩展欧几里得算法可以在求得 a、b 的最大公约数的同时，能找到一组整数解 x、y（其中一个很可能是负数），使他们满足 $$ax+by=gcd(a,b)$$ 。

我们知道，在欧几里得算法中我们仅仅利用了每步带余除法所得的余数，而扩展欧几里得算法中还利用了带余除法所得的商。扩展欧几里得算法可以用来计算模反元素（也叫模逆元），计算模反元素是 RSA  加密算法中获得所需公钥、私钥的必要步骤。

### 过程

在欧几里得算法中，我们记欲求最大公约数的两个数为 a、b，第 i 次的带余除法所得的商为 $$q_i$$ ，余数为 $$r_{i+1}$$ ，则欧几里得算法可以写成如下形式：
$$
r_0=a \\
r_1=b \\
.\\
.\\
.\\
r_{i+1}=r_{i-1}-q_ir_i
$$
当计算到 $$r_{i+1}=0$$ 时，计算结束。上一步得到的 $$r_i$$ 即为 a、b 的最大公约数。

而在扩展欧几里得算法中，再增加两组序列 $$s_i,t_i$$ ：
$$
r_0=a ,\ s_0=1,\ t_0=0\\
r_1=b ,\ s_1=0,\ t_1=1\\
.\\
.\\
.\\
r_{i+1}=r_{i-1}-q_ir_i,\ s_{i+1}=s_{i-1}-q_is_i,\ t_{i+1}=t_{i-1}-q_it_i
$$
结束的条件和欧几里得算法一致，即 $$r_{i+1}=0$$ ，此时所得的 $$s_i和t_i即满足\ gcd(a,b)=r_i=as_i+bt_i$$

### 实现

```python
def ext_euclid(a,b):
    old_s, s = 1, 0
    old_t, t = 0, 1
    old_r, r = a, b
    if b == 0:
        return 1,0,a
    else:
        while(r != 0):
            q=old_r // r
            old_r, r = r, old_r-q*r
            old_s, s = s, old_s-q*s
            old_t, t = t, old_t-q*t
    return old_s,old_t,old_r
```

