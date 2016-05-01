---
title: ubuntu SSL設定
toc: true
comments: true
date: 2016-04-28 19:59:50
description:
tags:
  - ubuntu
  - nginx
  - SSL
  - https
categories:
---

### 安裝 NGINX 伺服器
* 直接 ubuntu Server 直接可以透過apt-get套件管理安裝
```bash
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo install nginx
```

### 建立一個放憑證的folder
* 因為要透過nginx，所以直接在nginx的目錄下建一個folder
```bash
$ sudo mkdir /etc/nginx/ssl
```

### 產生自行簽署的 SSL 憑證
* 透過`openssl`產生自行簽署的憑證
```bash
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt
```
* 參數說明及設定參考這篇[NGINX 設定 HTTPS 網頁加密連線，建立自行簽署的 SSL 憑證](http://blog.gtwang.org/linux/nginx-create-and-install-ssl-certificate-on-ubuntu-linux/)

### 設定 nginx 伺服器
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
        ssl_certificate /etc/nginx/ssl/nginx.crt;
        ssl_certificate_key /etc/nginx/ssl/nginx.key;

        location / {
                proxy_pass http://app_server;
        }
}
```

### 重新啟動 nginx
```bash
$ sudo service nginx restart
```

### 透過 browser 連線
* 直接輸入 https://yourdomain 即可透過SSL連線，但因為是自行簽署的私人憑證並未透過第三方認證，正常來說會出現憑證授權不可靠的警告
