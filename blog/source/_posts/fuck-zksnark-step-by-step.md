---
title: 一步步解析 zk-snark
top: false
cover: false
toc: true
mathjax: true
date: 2020-09-16 13:41:12
password:
summary:
tags:
categories: blockchain | ZKP 
---







zk-SNARK ，即 “zero knowledge Succinct Non-interactive Argument of Knowledge” 的缩写。显而易见，这样的名字就像这门技术一样，是将一系列东西杂揉在一起。





当人们说到零知识证明时，要说这门技术做了什么，大家似乎都能说个七七八八出来，总结起来也就一句话：

**以不透露一个论断（`statement`）的任何信息为前提，向你证明这个论断是对的**。

但是知其然而不知其所以然，其中的原理是什么，大家似乎没办法解释出来，本文的宗旨即为了从其根本入手，一步步解析零知识证明这项技术的神秘之处。

  <!--more-->

## zk-SNARK

zk-SNARK ，即 “zero knowledge Succinct Non-interactive Argument of Knowledge” 的缩写。显而易见，这样的名字就像这门技术一样，是将一系列东西杂揉在一起。

* **zero knowledge：**零知识，即在证明的过程中不透露任何内情

* **succinct：**简洁的，主要是指验证过程不涉及大量数据传输以及验证算法简单

* **non-interactive：**无交互。此技术试图彻底避免 Prover 和 Verifier 之间需要经过多次交互才能取得满意的可靠性这一约束。

* **Arguments：**证明过程是计算完好（computationally soundness）的，Prover 无法在合理的时间内造出伪证（破解）。跟计算完好对应的是理论完好（perfect soundness)，密码学里面一般都是要求计算完好。

* **of knowledge：**对于一个 Prover 来说，在不知晓特定证明 (witness) 的前提下，构建一个有效的零知识证据是不可能的。

  

就像我们一步步剥离了 zk-SNARK 这个名字一样，现在我们来一步步揭开这项神秘且令人向往的技术。

### NP 与 P 问题

NP 与 P 问题

### Tate 配对



### ECA