---
title: 插值法综述
top: false
cover: false
toc: true
mathjax: true
date: 2020-08-18 23:04:55
password:
summary:
tags:
categories: Math
---



插值法的**中心思想**就是：

**在我们已具备一组 KV 键值对的情况下，如何得出还没被定到的区域的值**

使用插值法所建立的函数，在构造的函数中一定要重现原本给定的 KV 键值对，否则就不是插值法而是函数近似或者曲线拟合的问题了

插值的做法，直观来讲就是：

1. 先从 KV 键值对来获得函数 f(x)

2. 用函数 f(x) 求出我们所要的任何特定 x 之 f(x )  函数值。

<!--more-->

然而，比较精密且系统化的数值方法却不是用这两个步骤来进行插值，原因是前述两阶段方法**对于插值的精密度并没有控制**，效率较差，也比较会有进位误差。一般在做插值法，是从欲插值点 x 附近的几个 KV 键值对 xi 开始，建立插值函数 f(x) ，并且也试着网罗更多 KV 键值对来插值，看随着项数变多误差会不会变小，如此找出最适合的函数 f(x) 。

## 线性插值法

所有的插值法里面最简单的莫过于线性插值法，任两个相邻的点之间必可以拉一条直线把它们连起来，如此在之间的 x 值就都有线性函数 y(x ) 可以对应到，利用直线上的斜率必为固定值的特性

![2020-08-19_00-03](Interpolation/2020-08-19_00-03.png)

## 多项式插值法

### 线性方程

假设我们现在已知 k 个在二维平面上的点，那么我们可以连立这些点组成一个 k-1 次的方程组，从而解出这个方程组的各个系数。

但是线性方程组在实际应用中是有重大缺陷的：

1. 计算量大，如果是几万几十万的数据量，方程组的解将会非常耗时。
2. 如果要新增加一组数据，整个方程组就会发生改变，要重新计算

于是乎，我们引入了**牛顿插值法**

### 牛顿插值法

牛顿插值法的特点在于：**每增加一个点，不需要推翻之前的计算，只需要计算和新增加的点相关的多项式就可以了。**

假设已知 ![[公式]](https://www.zhihu.com/equation?tex=n%2B1) 个点相对多项式函数 ![[公式]](https://www.zhihu.com/equation?tex=f) 的值为：![[公式]](https://www.zhihu.com/equation?tex=%28x_0%2Cf%28x_0%29%29%2C%28x_1%2Cf%28x_1%29%29%2C%28x_2%2Cf%28x_2%29%29%2C+%5Ccdots+%2C%28x_+n%2Cf%28x_+n%29%29) ，求此多项式函数 ![[公式]](https://www.zhihu.com/equation?tex=f) 。

![v2-760da819b88578dde14769747402971a_720w](Interpolation/v2-760da819b88578dde14769747402971a_720w.png)

![v2-f5d582849a959ace34d56c6cf39dc124_720w](Interpolation/v2-f5d582849a959ace34d56c6cf39dc124_720w.jpg)

先从求满足两个点 ![[公式]](https://www.zhihu.com/equation?tex=%28x_0%2Cf%28x_0%29%29%2C%28x_1%2Cf%28x_1%29%29) 的函数 ![[公式]](https://www.zhihu.com/equation?tex=f_1%28x%29) 说起：

假设 ![[公式]](https://www.zhihu.com/equation?tex=f_1%28x%29%3Df%28x_0%29%2Bb_1%28x-x_0%29) ，

令 ![[公式]](https://www.zhihu.com/equation?tex=f_1%28x_1%29%3Df%28x_1%29) ：

![[公式]](https://www.zhihu.com/equation?tex=%5Cbegin%7Balign%2A%7D+%26+%5Cimplies+b_1%3D%5Cfrac%7Bf%28x_1%29-f%28x_0%29%7D%7Bx_1-x_0%7D+%5C%5C+%26+%5Cimplies+f_1%28x%29%3Df%28x_0%29%2B%5Cfrac%7Bf%28x_1%29-f%28x_0%29%7D%7Bx_1-x_0%7D%28x-x_0%29+%5Cend%7Balign%2A%7D%5C%5C)

现在我们增加一个点， ![[公式]](https://www.zhihu.com/equation?tex=%28x_0%2Cf%28x_0%29%29%2C%28x_1%2Cf%28x_1%29%29%2C%28x_2%2Cf%28x_2%29%29) ，求满足这三个点的函数 ![[公式]](https://www.zhihu.com/equation?tex=f_2%28x%29)：

假设 ![[公式]](https://www.zhihu.com/equation?tex=f_2%28x%29%3Df_1%28x%29%2Bb_2%28x-x_0%29%28x-x_1%29) ，

令 ![[公式]](https://www.zhihu.com/equation?tex=f_2%28x_2%29%3Df%28x_2%29)：


![[公式]](https://www.zhihu.com/equation?tex=%5Cbegin%7Balign%2A%7D+%26+%5Cimplies+b_2%3D%26+%26+%5Cfrac%7B%5B%5Cfrac%7Bf%28x_2%29+-+f%28x_1%29%7D%7Bx_2+-+x_1%7D%5D+-+%5B%5Cfrac%7Bf%28x_1%29+-+f%28x_0%29%7D%7Bx_1+-+x_0%7D%5D%7D%7Bx_2+-+x_0%7D+%5C%5C+%26+%5Cimplies+f_2%28x%29+%3D+%26+%26+f%28x_0%29%2B%5Cfrac%7Bf%28x_1%29-f%28x_0%29%7D%7Bx_1-x_0%7D%28x-x_0%29+%5C%5C+%26+%26+%26+%2B%5Cfrac%7B%5B%5Cfrac%7Bf%28x_2%29+-+f%28x_1%29%7D%7Bx_2+-+x_1%7D%5D+-+%5B%5Cfrac%7Bf%28x_1%29+-+f%28x_0%29%7D%7Bx_1+-+x_0%7D%5D%7D%7Bx_2+-+x_0%7D%28x-x_0%29%28x-x_1%29+%5Cend%7Balign%2A%7D%5C%5C)

![[公式]](https://www.zhihu.com/equation?tex=b_1%2Cb_2) 看起来蛮有特点的，我们把特点提炼一下。

一阶均差：

![[公式]](https://www.zhihu.com/equation?tex=f%5Bx_+i%2Cx_+j%5D%3D%5Cfrac%7Bf%28x_+i%29-f%28x_+j%29%7D%7Bx_+i-x_+j%7D%2Ci%5Cne+j%5C%5C)

二阶均差是一阶均差的均差：

![[公式]](https://www.zhihu.com/equation?tex=f%5Bx_+i%2Cx_+j%2Cx_+k%5D%3D%5Cfrac%7Bf%5Bi%2Cj%5D-f%5Bj%2Ck%5D%7D%7Bx_+i-x_+k%7D%2Ci%5Cne+j%5Cne+k%5C%5C)

三阶均差就是二阶均差的均差，以此类推，我们得到牛顿插值法为：

![[公式]](https://www.zhihu.com/equation?tex=%5Cbegin%7Balign%2A%7D+f%28x%29+%3D%26+f%28%7Bx_0%7D%29+%2B+f%5B%7Bx_0%7D%2C%7Bx_1%7D%5D%28x+-+%7Bx_0%7D%29+%5C%5C+%26+%2B+f%5B%7Bx_0%7D%2C%7Bx_1%7D%2C%7Bx_2%7D%5D%28x+-+%7Bx_0%7D%29%28x+-+%7Bx_1%7D%29+%2B%5Ccdots+%5C%5C+%26+%2B+f%5B%7Bx_0%7D%2C%7Bx_1%7D%2C+%5Ccdots+%2C%7Bx_%7Bn+-+2%7D%7D%2C%7Bx_%7Bn+-+1%7D%7D%5D%28x+-+%7Bx_0%7D%29%28x+-+%7Bx_1%7D%29+%5Ccdots+%28x+-+%7Bx_%7Bn+-+2%7D%7D%29%28x+-+%7Bx_%7Bn+-+1%7D%7D%29+%5C%5C+%26+%2B+f%5B%7Bx_0%7D%2C%7Bx_1%7D%2C+%5Ccdots+%2C%7Bx_%7Bn+-+1%7D%7D%2C%7Bx_+n%7D%5D%28x+-+%7Bx_0%7D%29%28x+-+%7Bx_1%7D%29+%5Ccdots+%28x+-+%7Bx_%7Bn+-+1%7D%7D%29%28x+-+%7Bx_+n%7D%29+%5Cend%7Balign%2A%7D%5C%5C)

计算通过下面这个示意图进行，就会很简单：

![v2-bb250de06e4ce4d88f31bfd7cc8b9df7_720w](/opt/src/github.com/Whisker17/blog-source/blog/source/_posts/Interpolation/v2-bb250de06e4ce4d88f31bfd7cc8b9df7_720w.jpg)

新增一个点就只需要计算相关的差分就可以了：

![v2-7caee6961c1c372e6743039b2ae32326_720w](/opt/src/github.com/Whisker17/blog-source/blog/source/_posts/Interpolation/v2-7caee6961c1c372e6743039b2ae32326_720w.jpg)



### 拉格朗日插值法



## Reference

1. [牛顿插值的几何解释是怎么样的](https://www.zhihu.com/question/22320408)
2. [如何直观的理解拉格朗日插值法](https://www.zhihu.com/question/58333118)
3. [如何通俗地解释泰勒公式](https://www.zhihu.com/question/21149770)