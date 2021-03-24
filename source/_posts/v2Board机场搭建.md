---
title: v2Board机场搭建
date: 2020-12-4
updated: 2020-12-4
categories:
- 黑盒子
tags:
- 黑盒子
---


## 前端面板[v2Board](https://github.com/v2board/v2board-docker)
如果内存<=1G,需要配置虚拟内存，[How to Add Swap Space on Ubuntu 18.04](https://linuxize.com/post/how-to-add-swap-space-on-ubuntu-18-04/)
```
$ git clone git@github.com:v2board/v2board-docker.git
$ cd v2board-docker
//同步子仓库
$ git submodule update --init --recursive
//启动docker
$ docker-compose up
//进入mysql容器里查看ip
$ docker exec -it v2board-docker_mysql_1 /bin/bash
# cat /etc/hosts

//进入v2board容器修改hosts
$ docker exec -it v2board-docker_www_1 /bin/bash
# vim /etc/hosts
写入mysql容器的host和ip以通信
//安装board
# wget https://getcomposer.org/download/1.9.0/composer.phar
# php composer.phar install
# php artisan v2board:install
数据库地址：填mysql容器的ip
数据库名：v2board
数据库用户名：root
数据库密码：v2boardisbest
完成
```
面板安装完成，输入地址访问。

## 配置
1. 配置节点
2. 配置后端 参[V2board搭建教程-后端Docker对接v2ray节点篇](https://zhujiget.com/4073.html)
3. 配置订阅

debug:
- 订阅无节点
v2board-docker的订阅地址的配置文件已不能适配新版clashX, 需要修改订阅地址的配置文件：
`vi app/Http/Controllers/Client/ClientController.php`
`Proxy` 改为 `proxies`
`'Proxy Group'`改为 `proxy_groups`
`Rule` 改为 `rules`
Done.

- 后台无debug日志
打开debug日志，修改.env文件 APP_DEBUG=true
执行`php artisan config:clear`和`php artisan env`来应用更改。
现在，使用postman访问接口能看到错误信息。

- 支付宝notify验签名失败
支付宝配置应该填入 应用私钥 + 支付宝公钥(而非应用公钥)

## 错误处理
`404 Site xxx.xxx.xxx.xxx is not served on this interface`
修改caddy.conf，把域名加到配置文件里

- docker里的alpine linux的cron定时任务不执行，不知道为什么
解决方法：在宿主机里创建定时任务执行
`* * * * * sudo docker exec v2boarddocker_www_1 php /www/artisan schedule:run`

## v2ray后端[aurora](https://github.com/tokumeikoi/aurora)


## 波塞冬后端（付费，50人内免费）
参考[](https://zhujiget.com/4073.html)


