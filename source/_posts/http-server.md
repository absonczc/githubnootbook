---
title: 开启本地服务器
categories:
  - Server
tags:
  - Server
date: 2020-05-15 14:47:22
mp3:
cover:
---

## 如何通过cmd 打开一个本地服务器

1. 首先你确认你电脑 是否有`nodejs`

没有node,可以进入 **[node官网 | NODE ](http://nodejs.cn/download/)** 下载

检查是否安装了node

``` bash
node -v
```

2. 接着安装全局本地服务器

``` bash
npm i http-server -g
```

3. 进入项目所在文件

``` bash
cd D:\note\20200429
```

> 输入后无法进入的话 再指定一下 进入(具体看一下cmd命令)

``` bash
cd D:
cd note\20200429
```

4. 令行输入http-server 即可在此文件下打开服务器

``` bash
http-server
```
