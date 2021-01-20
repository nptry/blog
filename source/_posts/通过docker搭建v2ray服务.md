---
title: 通过docker搭建v2ray服务
date: 2019-11-13
updated: 2019-11-13
categories:
- 黑盒子
tags:
- 黑盒子
---

## 获取镜像
`docker pull v2ray/official`

## 准备配置文件
需要在`/etc/v2ray`下创建`config.json`文件
这是一个最简单的config.json文件示例：
```
{
  "inbounds": [
    {
      "port": 8888,
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "b123456d-6324-4d53-ad4f-8cda48b30811",
            "alterId": 64
          }
        ]
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {}
    }
  ]
}
```

## 启动服务
docker run -it -d --name v2ray -v /etc/v2ray:/etc/v2ray -p [外部端口]:8888 v2ray/official v2ray -config=/etc/v2ray/config.json
例如：docker run -it -d --name v2ray -v /etc/v2ray:/etc/v2ray -p 20519:8888 v2ray/official v2ray -config=/etc/v2ray/config.json

## 配置v2ray客户端
id应与服务端的clients['id']一致
It should work now.
