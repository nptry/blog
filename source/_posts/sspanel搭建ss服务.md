---
title: sspanel搭建ss服务
categories:
- 黑盒子
tags:
- 黑盒子
---

## 前端面板添加ss节点
1. 节点地址填写后端ip
2. 节点ip不需要填
3. 只启用普通端口模式

## docker + 数据库方式 连接前端面板

```
docker run -d --name=ssrmu -e NODE_ID=4 -e API_INTERFACE=glzjinmod -e MYSQL_HOST=127.0.0.1 -e MYSQL_USER=root -e MYSQL_DB=airport -e MYSQL_PASS=password --network=host --log-opt max-size=50m --log-opt max-file=3 --restart=always fanvinga/docker-ssrmu
```

## 客户端
根据面板教程，订阅普通节点地址

参考：[SSPanel v3 mod 后端（Docker）对接](https://wiki.sspanel.host/#/ssrmu-docker)