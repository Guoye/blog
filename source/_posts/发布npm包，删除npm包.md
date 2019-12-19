---
title: 发布npm包，删除npm包
date: 2019-12-19 16:15:58
tags: [npm]
---
# 发布npm包
## 注册并在本机添加npm用户（已注册可忽略）
完成了上面的步骤之后，我们接下来要在www.npmjs.com注册一个账号，这个账号会被添加到npm本地的配置中，下面命令行将会使用到。

```shell
//前提已完成npm用户的注册
$ npm adduser
Username: your name
Password: your password
Email: yourmail@gmail.com
```

如果出现以下错误，可能是你的npm版本太低，通过sudo npm install -g npm升级一下。

```shell
npm WARN adduser Incorrect username or password
npm WARN adduser You can reset your account by visiting:
npm WARN adduser
npm WARN adduser     http://admin.npmjs.org/reset
npm WARN adduser
npm ERR! Error: forbidden may not mix password_sha and pbkdf2
npm ERR! You may need to upgrade your version of npm:
npm ERR!   npm install npm -g
npm ERR! Note that this may need to be run as root/admin (sudo, etc.)

```

成功之后，npm会把认证信息存储在~/.npmrc中，并且可以通过以下命令查看npm当前使用的用户：

```shell
$ npm whoami
```
以上完成之后，我们终于可以发布自己包了。

# 发布 
```shell
$ npm publish 
```

# 删除
```shell
$ npm unpublish --force //强制删除
```
```shell
$ npm unpublish guitest@1.0.1 //指定版本号
```
```shell
$ npm deprecate //某些情况
```