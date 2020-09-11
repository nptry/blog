---
title: vps测速
date: 2020-09-07
updated: 2020-09-07
categories:
- Linux
tags:
- Linux
---

* 使用 `speedtest-cli` 工具

## 安装
```
sudo apt-get update
sudo apt-get install python-pip
sudo pip install speedtest-cli
```
## 使用

测试服务器速度
```
$ speedtest-cli
```

显示speedtest.net的测试服务器列表
```
$ speedtest-cli --list
$ speedtest-cli --list | grep China
```

测试vps到特定测试服务器速度
```
$ speedtest-cli --server SERVER_NO
```
