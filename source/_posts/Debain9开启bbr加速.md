---
title: Debain9开启bbr加速
date: 2019-11-13
updated: 2019-11-13
categories:
- 黑盒子
tags:
- 黑盒子
---

## 方法

**1. 修改系统变量**
```
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
```

**2. 保存生效**
```
sysctl -p
```

**3. 查看内核是否已开启BBR**
```
sysctl net.ipv4.tcp_available_congestion_control
```
显示以下即已开启：
```
# sysctl net.ipv4.tcp_available_congestion_control
net.ipv4.tcp_available_congestion_control = bbr cubic reno
```
**4. 查看BBR是否启动**
```
lsmod | grep bbr
```
显示以下即启动成功：
```
# lsmod | grep bbr
tcp_bbr                20480  14
```

内容来自[Debian 9/10快速开启Google BBR的方法，实现高效单边加速](https://www.moerats.com/archives/297/)


