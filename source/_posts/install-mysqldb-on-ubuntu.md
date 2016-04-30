---
title: 在ubuntu上安裝mysql db
comments: true
date: 2016-04-27 14:41:31
tags:
  - mysql
  - ubuntu
toc: true
description: 這篇是描述如何在ubuntu上安裝mysql的過程
categories: mysql
---
### 透過 apt-get 安裝

```bash
#更新apt-get 套件
$ sudo apt-get update
$ sudo apt-get upgrade

#安裝mysql
$ sudo apt-get install mysql-server
```
### 安裝 mysql_secure_installation

```bash
$ sudo mysql_secure_installation
```

### 調整可連線的IP

* 一般預設都是只能給本機(127.0.0.1)連線，如果要給外部的ip連線則需修改設定檔

```xml
#/etc/mysql/my.cnf

...
#允許任意ip連線
bind_address = 0.0.0.0
...

```

### 注意事項
* 安裝完mysql預設的port是3306
* 如果ubuntu是aws 的 ec2 則需注意security group是否有開起mysql的port 3306
