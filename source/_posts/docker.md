---
title: docker基础
date: 2020-11-25
updated: 2020-11-25
categories:
- Docker
tags:
- Docker
---
image就像方便面，在任何地方都可以放上佐料，泡上水，就是一碗热腾腾的泡面出来了，你还可以加点其他的佐料，泡好的泡面就相当于运行中的container。

# 参考

[阮一峰 Docker 入门教程](https://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)

# 笔记

## 常用命令
`docker ps` 或 `docker container ls`
`docker container list -a`
`docker container stop [containerID]`
`docker container rm [containerID]`

查看日志
`docker container logs [containerID]` 

进入一个容器
`docker container exec -it [containerID] /bin/bash`

提交对容器的修改
`docker commit [选项] <容器ID或容器名> [<仓库名>[:<标签>]]`
例如：
`docker commit -m "config mysql" 3e16e505a3b2 thiagobarradas/lamp:php-5.6`

参数
-v local_file_path:docker_path 把本地文件映射到docker里


## docker hub
在[docker hub](https://hub.docker.com)注册后，可创建一个免费仓库
在命令行运行`docker login`登录后可将image上传到仓库
`docker pull [imageName]`


## 容器间的通信
每个容器有自己的内部ip，可`cat /etc/hosts`查看
如果A容器想要访问B容器的服务，可直接在A的hosts里写入B的ip即可。
在docker-compose文件中，是*`extra_hosts`*这个参数。
