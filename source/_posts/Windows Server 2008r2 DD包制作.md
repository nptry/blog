---
title: Windows Server 2008r2 DD包制作
date: 2019-06-30
updated: 2019-06-30
categories:
- Windows
tags:
- Windows
---

参照
[秋水-DD包制作](https://teddysun.com/544.html) 和 [DD包制作](https://www.fmqcloud.com/archives/makedd.html)

重点：
1. 修改3389端口
2. 打开远程服务
3. 修改IE安全性
4. 关闭Ctrl+Alt+Del激活
5. 使用Hyper-V优化配置，关闭密码过期，安装Chrome


# linux 安装脚本
```
#!/bin/sh

wget --no-check-certificate -qO InstallNET.sh "https://shell.p1e.cn/reinstall/InstallNET.sh" && bash InstallNET.sh -dd 'DD包http直链地址'
```