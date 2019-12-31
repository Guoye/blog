---
title: Nginx配置大文件上传
categories:
  - nginx
date: 2019-12-31 15:15:29
tags:
---

# nginx问题
遇到的问题：
- Nginx: 413 – Request Entity Too Large Error and Solution
- TIMEOUT

# 解决方法
解决方法：在nginx的配置文件下（通常为xxx.conf），加上以下配置：

```
client_max_body_size     50m;  # 限制请求体的大小，若超过所设定的大小，返回413错误，默认1m
client_header_timeout    1m;  # 读取请求头的超时时间，若超过所设定的大小，返回408错误
client_body_timeout      1m; # 读取请求实体的超时时间，若超过所设定的大小，返回413错误
proxy_connect_timeout     60s; # http请求无法立即被容器(tomcat, netty等)处理，被放在nginx的待处理池中等待被处理。此参数为等待的最长时间，默认为60秒，官方推荐最长不要超过75秒
proxy_read_timeout      1m;  # http请求被容器(tomcat, netty等)处理后，nginx会等待处理结果，也就是容器返回的response。此参数即为服务器响应时间，默认60秒
proxy_send_timeout      1m; # http请求被服务器处理完后，把数据传返回给Nginx的用时，默认60秒
```

```shell
server {
    listen       80;
    server_name  localhost;
    
	client_max_body_size     10m;
	client_header_timeout    5m;
	client_body_timeout      5m;
	proxy_connect_timeout     6000s;
	proxy_read_timeout      5m;
	proxy_send_timeout      5m;

	location  / {
		# ...
	}
}	
```

# 重启nginx
设置完成后，需要使用 `reload` 或者`reload`重启nginx