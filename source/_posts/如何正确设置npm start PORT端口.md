---
title: 如何正确设置npm start PORT端口(windows/mac)
date: 2019-12-19 16:16:01
tags: [npm, set]
---

# 正确设置PORT端口(windows/mac)
在跑lesson5的时候，有部分同学会遇到以下错误，这是由于不同系统，所执行的命令代码有所差异。
查看图片：​​
https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy85NDE4MjkyLTVmMDYxYjRlYzI1NWJkY2YucG5n


# MAC/linux环境：
```shell
$ PORT=8081 npm start
```

使用上面命令每次都需要重新设置

如果想设置一次永久生效，使用下面的命令。

```shell
$ export PORT=8081  
```
```shell
$ npm start
```

# Window系统环境，按照顺序这样进行：
```shell
$ set PORT=8081
```
```shell
$ npm start
```
关闭命令行窗口后，端口的配置会失效