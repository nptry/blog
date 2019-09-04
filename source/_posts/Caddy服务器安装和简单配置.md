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

# php-fpm 的 Caddyfile 配置

www.nptry.xyz {
    root /var/www/airport/public
    rewrite {
		  to {path} {path}/ /index.php
		}
    fastcgi / /run/php/php7.3-fpm.sock php {
        index index.php index.html
    }
}

参考 ![使用 CADDY 代替 NGINX](https://imnerd.org/use-caddy-replace-nginx.html)