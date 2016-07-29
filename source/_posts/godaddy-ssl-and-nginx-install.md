---
title: go daddy買ssl & Nginx 安裝
toc: true
comments: true
date: 2016-07-21 08:21:15
description:
tags:
    - SSL
    - nginx
categories: ubuntu
---
### 在本機產生憑證
* 透過openssl 產生憑證檔
``` bash
openssl req -new -newkey rsa:2048 -nodes -keyout yourdomain.key -out yourdomain.csr
```
* 輸入申請資料 常用名/機構/組織/城市/州或省/國家 等等資訊

### godaddy domain 管理介面
* 開始剛剛產生的`.csr`檔案，在godaddy的介面上輸入

### 從godaddy下載SSL憑證檔案

### 安裝至nginx伺服器上
* 需先將剛下載的兩個檔案合併為一個檔
* 安裝是nginx上，設定如下

### 設定 nginx 伺服器
* 需先將剛下載的兩個檔案合併為一個檔
```bash
$ sudo cat your_domain_name.crt DigiCertCA.crt >> bundle.crt
```
* 編輯 nginx 的設定檔
```bash
$ sudo vi /etc/nginx/sites-available/default
```
* 加入以下設定
```txt
upstream app_server {
    server 127.0.0.1:8080 fail_timeout=0;
}

server {
        listen 443;
        server_name localhost;

        #root html;
        #index index.html index.htm;

        ssl on;
        #設定憑證金鑰的路徑
        ssl_certificate bundle.crt;
        ssl_certificate_key yourdomain.key;

        location / {
                proxy_pass http://app_server;
        }
}
```

### 重新啟動 nginx
```bash
$ sudo service nginx restart
```
