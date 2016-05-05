---
title: npm 基本指令
toc: true
comments: true
date: 2016-05-01 15:19:35
description:
tags:
  - npm
categories:
  - node.js
---
### npm 簡介
* npm 全名為 Node Package Manager，是 Node.js 的套件（package）管理工具

* 產生package.json 檔案
```bash
$ npm init
```
* 如果專案裡已有package.json可以直接執行 install
```bash
$ npm install
```
* 全域安裝加上`-g`的參數
```bash
$ npm install <package name> -g
```

* 專案安裝不加`-g`的參數
```bash
$ npm install <package name>
```

* 專案安裝並加入`package.json`檔案裡，需加上`--save`的參數
```bash
$ npm install <package name> --save
```

* 定義在`package.json`檔案裡`scripts`參數下的指令可透過`npm start`執行
```xml
#package.json

...
"scripts": {
    "start": "node ./bin/www"
}
...

```
```bash
#實際上是執行 $ node ./bin/www
$ npm start
```
