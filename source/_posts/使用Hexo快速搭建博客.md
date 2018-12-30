---
title: 使用Hexo快速搭建博客
categories:
- 集装箱
tags:
- hexo
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

## 使用分类和标签功能
我们发现左侧有分类和标签两个入口，但是不能点击，因为默认没有打开。
创建标签页面：
```
$ hexo new page "tags"
```
编辑标签页面`source/tags/index.md`：
```
---
title: tags
date: 2018-12-30 20:59:40
type: "tags"
---
```

创建分类页面：
```
$ hexo new page "categories"
```
编辑分类页面`source/categories/index.md`：
```
---
title: categories
date: 2018-12-30 20:59:40
type: "categories"
---
```

刷新页面发现左侧分类和标签两个功能可用了。

在文章中我们可以这样添加分类和标签：
```
---
title: 使用Hexo快速搭建博客
categories:
- 集装箱
tags:
- hexo
---
```

如果我们添加多个分类或标签后再删除，会发现其统计数量不对，这时需要清理缓存：
1. 删除站点目录下的db.json
2. `$ hexo clean`
3. `$ hexo g`






