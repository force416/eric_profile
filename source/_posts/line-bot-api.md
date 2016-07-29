---
title: Line機器人API
toc: true
comments: true
date: 2016-07-28 23:36:08
description:
tags:
    - Line
categories:
    - Java
---
### 註冊申請Line 機器人
* [Line developer 官網](https://developers.line.me/bot-api/overview) 申請機器人帳號
* 申請註冊channel後，設定`Callback URL`，必需要是`https`而且不能是自行簽署的憑證，還要符合line認可的[CA list](https://developers.line.me/wp-content/uploads/2016/04/ca_root.txt)
* 還需在`Server IP Whitelist` 加上你提供callback url的主機ip
* 取得API需使用的三組代碼`Channel ID` `Channel Secret` `MID`

### 開始撰寫機器人程式
* 推薦使用[java sdk](https://github.com/line/line-bot-sdk-java)

### 個人github sample
* (https://github.com/force416/linebot)
