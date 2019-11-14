---
title: Caddy服务器 + php-fpm配置
categories:
- 后端
tags:
- 后端
---

# 安装

打开官网： https://caddyserver.com/download 在左侧点击`Add plugins`
选择一个或几个DNS SERVER，否则caddy在获取ssl证书的时候，可能会出现无法解析域名的错误。

复制网页底下的 `One-step installer script`并在服务器运行，如：
```
$ curl https://getcaddy.com | bash -s tls.dns.cloudflare,tls.dns.googlecloud
```

# 配置

首先我们为 Caddy 创建一个配置目录，这里以 /etc/caddy 为例。同时我们还需要生成一个目录用来给 Caddy 放置网站证书。
```
# mkdir /etc/caddy
# mkdir /etc/caddy/conf
# echo 'import ./conf/*' >> /etc/caddy/Caddyfile
# mkdir /etc/ssl/caddy
```

# php-fpm 的 Caddyfile 配置

`vim /etc/caddy/conf/airport`
```
www.nptry.xyz {
  root /var/www/airport/public
	rewrite {
	  to {path} {path}/ /index.php
	}
  fastcgi / /run/php/php7.3-fpm.sock php {
		ext .php
		split .php
    index index.php
  }
}
```

##验证
`# caddy` 应该能启动服务


## 后台启动
`# nohup caddy &`

参考 [使用 CADDY 代替 NGINX](https://imnerd.org/use-caddy-replace-nginx.html)