---
title: SSPanel-Uim机场搭建教程
categories:
- 黑盒子
tags:
- 黑盒子
---

## 前端面板程序安装与部署
[前端安装](https://github.com/Anankke/SSPanel-Uim/wiki/%E5%89%8D%E7%AB%AF%E5%AE%89%E8%A3%85)
施工中...🚧

## v2ray后端程序

[v2ray Rico 版使用教程](https://github.com/Anankke/SSPanel-Uim/wiki/v2ray---Rico-%E7%89%88%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B)

### 在前端面板里添加节点
节点地址：eg: 服务端ip;9517;16;kcp;;
** 注意： IOS客户端 Shadowrock 和 Pepi 都不支持kcp **
kcp是一种用带宽换速度的协议，加速UDP数据流。
bbr也是用带宽换速度，加速TCP数据流，因为是服务器部署，所以是单边加速，从服务器到客户端的数据包都是双倍的。

`单端口多用户启用` 项选择 `只启用普通端口`
`节点类型` 选择 `v2ray`

点击添加，完成前端节点添加。

### 后端v2ray的安装
docker方式部署，需要服务器支持docker, 低配openvz的vps很难安装。

执行
```
mkdir v2ray-agent  &&  \
cd v2ray-agent && \
curl https://raw.githubusercontent.com/rico93/v2ray-sspanel-v3-mod_Uim-plugin/master/install.sh -o install.sh && \
chmod +x install.sh && \
bash install.sh
```
install => sspanel_url(前端面板地址) => panel_key(muKey, 前端的配置文件`.Config`里可查) => 节点ID(面板创建节点的ID) => 其它默认

后端默认以2333端口接收来自面板的查询及设置请求。

`$ netstat -lan |grep 2333 ` 可见服务器对2333端口的监听。

后端安装好后，面板的节点状态图标将显示为在线。此时不同的面板用户可以获取不同的vmess链接。默认流量上线1G，流量用完后将不能连接。




