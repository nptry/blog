---
title: 使用Hexo快速搭建博客
---
[Hexo官网](https://hexo.io/)

## 安装
``` bash
$ npm install hexo-cli -g
```

## 快速开始

### 创建博客应用

``` bash
$ hexo init blog
$ cd blog
```

### 运行服务

``` bash
$ hexo server
```
默认会监听本地4000端口，浏览器打开localhost:4000便可预览。

## 部署
这里只说部署到自己的服务器
修改blog目录下的`_config.yml`文件
```
deploy:
  type: rsync
  host: [house]
  user: [user]
  root: ['/var/www/blog']
  port: 22
  delete: true
  verbose: true
  ignore_errors: false
  args: --rsync-path=sudo rsync
```

执行命令`$ hexo deploy`可以将文件部署到服务器上。

## 服务器部分

### 配置nginx
```
server {
        listen       80;
        server_name  www.nptry.com;
        root   /var/www/blog;
        charset utf-8;
        location / {
            root   /var/www/blog;
            index  index.html;
        }
    }
```

### 配置https
可先从[freessl](https://freessl.cn/)申请免费的ssl证书，获得.pem和.key两个证书文件。
```
server {
    #ssl参数
    listen              443 ssl;
    server_name         www.nptry.com;
    root   /var/www/blog;

    ssl_certificate /etc/ssl/certs/www.nptry.com.pem;
    ssl_certificate_key /etc/ssl/certs/www.nptry.com.key;
}
```
重启nginx后便可通过https访问blog了。

## 更换主题
我这里将默认主题换成了[NexT](https://github.com/iissnan/hexo-theme-next)的Pisces风格

在theme目录里下载了Next主题后，修改`_config.yml`文件：
```
...
theme: next
...
```
修改Next主题风格，修改`themes/next/_config.yml`文件：
```
...
# Schemes
# scheme: Muse
#scheme: Mist
scheme: Pisces
#scheme: Gemini
...
```
然后重新生成静态文件
```
$ hexo generate
```
重新部署后即生效
```
$ hexo deploy
```




