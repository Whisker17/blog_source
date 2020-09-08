---
title: 探索椭圆曲线配对
top: false
cover: false
toc: true
mathjax: true
date: 2020-09-07 11:36:45
password:
summary:
tags:
categories: blockchain | ZKP | 翻译
---



原文：[Exploring Elliptic Curve Pairings](https://medium.com/@VitalikButerin/exploring-elliptic-curve-pairings-c73c1864e627)

  <!--more-->

# 探索椭圆曲线配对

椭圆曲线配对是各种构造背后的关键密码学原语之一，包括确定性阈值签名，zk-SNARK 和其他更简单形式的零知识证明。 椭圆曲线配对（或“双线性图”）是使用椭圆曲线进行加密应用（包括加密和数字签名）已有30年历史的最新成果。 配对引入了一种“加密乘法”形式，极大地扩展了基于椭圆曲线的协议的功能。 本文的目的是详细介绍椭圆曲线配对，并解释其工作原理的概述。
第一次阅读甚至第十次阅读时，你都可能无法了解所有内容； 这东西真的很难。 但是希望本文至少可以使您对幕后发生的事情有所了解。

椭圆曲线本身是一个不容易理解的话题，本文通常假定您知道它们是如何工作的。 如果不这样做，我建议您在此作为入门文章：https://blog.cloudflare.com/a-relatively-easy-to-under-understand-primer-on-elliptic-curve-cryptography/。 简要总结一下，椭圆曲线密码学涉及称为“点”的数学对象（这些点是具有（x，y）坐标的二维点），并具有用于加和减的特殊公式（即，用于计算R = P + Q），也可以将一个点乘以一个整数（即P * n = P + P +…+ P，但是如果 n 很大的话，则有一种更快的计算方法）。

![](ECC-pairings/1_2PxXNwMceh1XC_waAP9NiA.jpeg)



存在一个特殊的点，称为“无穷大点”（O），在点算术中即为零。 即 P + O = P。此外，曲线具有“阶数”；存在一个数字 n ，使得任何P都为P * n = O（当然，P *（n + 1）= P，P *（7 * n + 5）= P * 5，依此类推）。也有一些公认的“生成元” G，从某种意义上讲，生成元 G 代表数字1。理论上，曲线上的任何点（O除外）都可以是 G ；重要的是 G 是标准化的。
配对更进一步，它们使您可以检查椭圆曲线点上某些更复杂的方程式——例如，如果 P = G * p，Q = G * q 和 R = G * r ，当我们只有 P，Q 和 R 作为输入时，也可以检查是否 p * q = r 。这种形式看起来似乎椭圆曲线的基本安全保证已被破坏，因为关于 p 的信息是在我们只知道 P 的情况下而泄漏的，而事实证明泄漏是高度包含的——具体来说，[决策Diffie Hellman问题](https://en.wikipedia.org/wiki/Decisional_Diffie%E2%80%93Hellman_assumption)很容易，但是计算 Diffie Hellman 问题（在上面的示例中知道 P 和 Q ，计算 R = G * p * q ）和离散对数问题（从 P 中恢复 p ）在计算上仍然不可行（至少在以前是这样）。

观察配对功能的第三种方法，也许对于我们所使用的大多数用例而言，最能说明问题的是，如果您将椭圆曲线点视为单向加密数字（即，encrypt（p） = p * G = P），则传统的椭圆曲线数学让您检查数字的线性约束（例如，如果已知 P = G * p，Q = G * q 和 R = G * r ，则检查 5 * P + 7 * Q = 11 * R 实际上是在检查 5 * p + 7 * q = 11 * r ），配对使您可以检查二次约束（例如，检查e(P，Q) * e(G，G * 5) = 1 确实在检查 p * q + 5 = 0 ）。 升到二次就足以让我们使用确定性门限签名，QAP 和所有其他好东西。
现在，我们上面介绍的这个有趣的 e(P，Q) 运算符是什么？ 这就是配对。 数学家有时也称它为双线性图。 这里的“双线性”一词基本上意味着它满足约束条件：

e(P, Q + R) = e(P, Q) * e(P, R)

e(P + S, Q) = e(P, Q) * e(S, Q)

