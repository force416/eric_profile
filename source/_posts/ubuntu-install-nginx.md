---
title: ubuntu上安裝Nginx
toc: true
comments: true
date: 2016-05-08 10:55:55
description:
tags:
categories: ubuntu
---
### Nginx 介紹
* Nginx 是個 Reverse Proxy Server(反向代理伺服器)，為什麼叫反向代理呢? 因為相對於一般 Proxy Server(正向代理伺服器)做的事剛好相反，用一張圖來解釋[(圖片出處)](https://www.zhihu.com/question/24723688)
{% asset_img proxy_server.jpg %}

### 在 ubuntu 上透過 apt-get 安裝 Nginx
```bash
$ sudo apt-get update
$ sudo apt-get install nginx
```

### Nginx 設定
* 基本的配置文件都在 `/etc/nginx` 路徑底下
* 主要的置文件 `/etc/nginx/sites-available/default`

### Nginx command line
* start
```bash
$ sudo service nginx start
```
* stop
```bash
$ sudo service nginx stop
```
* restart
```bash
$ sudo service nginx restart
```
* 重新讀取配置文件
```bash
$ sudo service nginx -s reload
```
