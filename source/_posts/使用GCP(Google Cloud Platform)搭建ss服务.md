---
title: 使用GCP(Google Cloud Platform)搭建ss服务
categories:
- 黑盒子
tags:
- 黑盒子
---

## 第一步：撸个GCP
1. 拥有一个新的gmail邮箱(现在要验证手机号，中国号码很早就不行了，美国虚拟号码现在也不行了，可以去某宝买一个，省事)
2. [GCP免费试用](https://cloud.google.com/free-trial)，从这个地址去试用。我这次是用的[别人的推广链接](https://www.v2ex.com/t/600029#reply5)注册的，在GCP这一步没有验证手机号，使用之前薅了两次的招行全币信用卡，完成了信用卡验证。

## 第二步：创建服务器
### 选个好的服务器节点
1. 今天测试结果，台湾地区的ping值最低，虽然要绕香港，但是延迟比香港节点的低，不知道为什么。
2. [在线路由追踪工具](https://tools.ipip.net/traceroute.php)
3. 同样是台湾节点，不同的ip，丢包率不一样，好的ip丢包率在1%以下，试了好多ip都是7%左右的丢包率，丢包率对最后的ss效果影响很大，这里一定要挑到一个好的ip。

### 操作
1. 创建服务器的时候，选择台湾地区，我这次选的tw的east1-c区域的机器，选到了一个稳定的ip。创建的时候修改磁盘为SSD，大小为15G，我觉得10G小了点（因为要装点其它的程序）
2. 操作系统选debain 9，debain是ubuntu的原型，开源社区支持更多。
3. 创建完后得到ip，测试这个ip，ok则进行下一步
4. 配置ssh key，以便从终端访问服务器
5. 配置防火墙，允许所有流量通过 `0.0.0.0/0`，简单粗暴
6. done

## 第三步：安装ss服务
1. 选择一个ss软件，我这里选用的[ss-libev](https://github.com/shadowsocks/shadowsocks-libev)，不为什么，就是看它star多，能用就行
2. 使用docker方式安装，用docker不会把系统搞乱，管理起来方便。[debian9安装docker](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-debian-9)
3. docker安装ss-libev，参数含义见[README](https://github.com/shadowsocks/shadowsocks-libev#docker)
```
docker pull shadowsocks/shadowsocks-libev
docker run -e PASSWORD=password -e METHOD=aes-256-cfb -p 30519:8388 -p 30519:8388/udp -d --restart always shadowsocks/shadowsocks-libev
```
4. `docker container ps`查看，服务应该已经开启
5. 其它docker命令
`docker ps -a --no-trunc` 查看docker运行的command的全语句
`docker exec [container_id] bash -c 'echo "$ENV_VAR"'` 显示环境变量
6. 配置ss客户端，填写正确的参数，It should be work now.



