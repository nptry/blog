---
title: 安卓手机使用TWRP方式刷机
date: 2020-07-28
updated: 2020-07-28
categories:
- 折腾
tags:
- 折腾
---

# 第一步：刷入TWRP

1. 电源键 + 音量减 进入fastboot模式
2. 下载twrp一键刷入recovery工具
3. 运行recovery工具，按照说明刷入手机，这时系统可以识别手机存储
4. 使用twrp做四清(或双清）操作，cache system ..
5. 把rom包复制到手机存储，使用twrp安装这个包
6. 安装完成后，不要立即重启，选择清理，再清理一次。
7. 完成。