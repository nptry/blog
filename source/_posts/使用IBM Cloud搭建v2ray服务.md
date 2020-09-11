---
title: 使用IBM Cloud搭建v2ray服务
date: 2020-09-10
updated: 2020-09-10
categories:
- 黑盒子
tags:
- 黑盒子
---

## 参照
[IBMYes](https://github.com/CCChieh/IBMYes)

## 注意事项
1. 我使用的时候，创建Go应用失败，选择的创建Ruby应用，也能运行教程里的脚本
2. Mac上我使用的v2ray客户端是[Mellow](https://github.com/mellow-io/mellow)
3. 项目当前（2020-09-10）版本有个错误，项目脚本在配置服务端v2ray时并没有使用path值，而生成的vmess链接里却加上了path值，导致不能使用，可先将客户端path值去掉。
4. vmess链接转换为对应的json文件为：
```
{
    "log": {
        "access": "",
        "error": "",
        "loglevel": "error"
    },
    "inbounds": [
        {
            "tag": "socks-in",
            "port": 1080,
            "listen": "::",
            "protocol": "socks",
            "settings": {
                "auth": "noauth",
                "udp": true,
                "ip": "127.0.0.1"
            }
        }
    ],
    "outbounds": [
        {
            "protocol": "vmess",
            "settings": {
                "vnext": [
                    {
                        "address": "cloudflare.com",
                        "port": 443,
                        "users": [
                            {
                                "email": "user@v2ray.com",
                                "id": "bcde1f3a-cccc-4d79-8a2b-25860dccecec",
                                "alterId": 4,
                                "security": "auto"
                            }
                        ]
                    }
                ]
            },
            "streamSettings": {
                "network": "ws",
                "security": "tls",
                "tlsSettings": {
                     "allowInsecure": false,
                     //伪装域名Host
                     "serverName": "shiny-forest-95e2.hansi.workers.dev"
                },
                "wsSettings": {
                    "connectionReuse": true,
                    "path": "",
                    "headers": {
                    		//伪装域名Host
                        "Host": "shiny-forest-95e2.hansi.workers.dev"
                    }
                }
            },
            "mux": {
                "enabled": true
            },
            "tag": "proxy"
        },
        {
            "protocol": "freedom",
            "tag": "direct",
            "settings": {
                "domainStrategy": "UseIP"
            }
        }
    ],
    "dns": {
        "servers": [
            "1.0.0.1",
            "localhost"
        ]
    },
    "routing": {
        "domainStrategy": "IPIfNonMatch",
        "rules": [
            {
                "type": "field",
                "ip": [
                    "geoip:private",
                    "geoip:cn"
                ],
                "outboundTag": "direct"
            },
            {
                "type": "field",
                "domain": [
                    "geosite:cn"
                ],
                "outboundTag": "direct"
            }
        ]
    }
}
```
5. 详细了解v2ray，见[Project V](https://www.v2ray.com/)
6. 套cloudflare前，speedtest测速只有几M，套cloudflare后，测速可达百M
7. mac下查看端口 `$ lsof -i:1080`