---
title: Chrome允许http获取摄像头和麦克风授权
date: 2019-01-05
updated: 2019-01-05
categories:
- 集装箱
tags:
- 大杂烩
---

考虑安全因素，chrome禁用了对http站点的摄像头和麦克风授权。但是我们开发是需要本地调试，就需要关闭这个限制。

浏览器打开`chrome://flags/#unsafely-treat-insecure-origin-as-secure`

启用如图选项，填写白名单地址，重启浏览器即可。

![](https://hans-blog.oss-cn-beijing.aliyuncs.com/p1.png)
