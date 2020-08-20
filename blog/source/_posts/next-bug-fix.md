---
title: Blog 搭建错误总结
top: false
cover: false
toc: true
mathjax: true
date: 2020-08-10 21:16:00
password:
summary:
tags:
categories: blog
---





在本篇 Blog 中将会对在部署过程中发现的问题进行总结

## 访客计数出错

* **错误场景：**

在使用 LeanCloud 时，发现填入 AppId 以及 AppKey 之后阅读数量出错，错误代码为

```
Counter not initialized! More info at console err msg.
```

* **解决方案：**

1. 将 `security` 字段改为 `false`
2. 安装了插件`hexo-leancloud-counter-security`（命令行执行`npm install hexo-leancloud-counter-security`）

  <!--more-->