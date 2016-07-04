---
title: docker 基本教學
toc: true
comments: true
date: 2016-07-04 11:37:01
description:
tags:
categories: docker
---
### docker 介紹
* 關於docker 可以用張圖片解釋 [圖片出處](https://hackpad.com/ep/pad/static/ZwP4hGtPaJB)
{% asset_img docker_img.jpg %}

* 基本上要搞清楚 `host`、`image`、`container`、`dockerfile`之間的關係

* [docker官網的Repositories](https://hub.docker.com/)
提供`imgae`下載，包含`ubuntu`、`mysql`、`mongodb`各式image

### docker install
* [官網 ubuntu docker 安裝教學](https://docs.docker.com/engine/installation/linux/ubuntulinux/) 各版本的linux安裝方式各有不同

### docker cli
* 最基本的docker run 執行一個`ubuntu` (:後面是image的tag版本14.04)的`container` 印出Hello world
``` bash
$ docker run ubuntu:14.04 /bin/echo 'Hello world'
Hello world
```
* 更多指令在終端機執行docker 就會列出有哪些指令可以用了

### docker 參考
(https://docs.docker.com/) docker官網文件
(https://www.gitbook.com/book/philipzheng/docker_practice/details)《Docker —— 從入門到實踐­》
