---
title: Nginx配置404自定义页面
categories:
  - nginx
date: 2019-12-31 18:06:49
tags:
---


# 1. 修改nginx.conf http
nginx.conf 文件http 区域添加 `fastcgi_intercept_errors on;`

```
http {
    .......
    fastcgi_intercept_errors on;
```

# 2. 配置conf server
配置`error_page 404 `
```
server {
	listen 80;
	server_name www.zhangguoye.com;
	index index.html index.htm;
	root /home/wwwroot;
 
	error_page 404 /404.html;
	location = /404.html {
                root   /home/wwwroot/;  # 在此目录下添加自定义的404.html
    }
```

# 3. 重启nginx
使用`restart` 或者 `reload` 重启nginx，使配置生效。