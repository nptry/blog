---
title: Ubuntu防止ssh自动断开
date: 2019-01-13
updated: 2019-01-13
categories:
- Linux
tags:
- Linux
---

当我们访问云服务器时，ssh经常自动断开，很不方便，如何防止自动断开呢。
## 方法一：修改客户端配置
修改本机`/etc/ssh/ssh_config`文件，添加如下参数
```
ServerAliveInterval 60
```
客户端每60秒便会向服务器发送空包以保持连接。

## 方法二：修改服务器配置
修改服务器`/etc/ssh/sshd_config`文件，添加如下参数
```
ClientAliveInterval 600
ClientAliveCountMax 10
```
服务器每600秒会向客户端发送空包以保持连接，`600*10 = 6000秒 = 100分钟` 后客户端依然无响应将会断开连接。

