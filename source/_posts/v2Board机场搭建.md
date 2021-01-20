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

## 错误处理
`404 Site xxx.xxx.xxx.xxx is not served on this interface`
修改caddy.conf，把域名加到配置文件里

## v2ray后端[aurora](https://github.com/tokumeikoi/aurora)


## 波塞冬后端（付费，50人内免费）