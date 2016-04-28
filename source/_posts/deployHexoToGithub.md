---
title: 在github上架設hexo
date: 2016-04-26 12:56:26
tags:
	- github
	- hexo
categories: github
comments: true
toc: true
description: 這篇是在講如何在github的靜態頁面上架設hexo blog framework
---
### 申請github帳號

### install nodejs
* 上[nodejs](https://nodejs.org/en/)的官網下載並安裝

### npm install hexo
* 上[hexo](https://hexo.io/zh-tw/)的官網有安裝教學

```bash
$ npm install hexo-cli -g
$ hexo init blog
$ cd blog
$ npm install
$ hexo server
```

### 在github上建立repositories
* 建立的專案名稱eric_profile

### 將專案發佈上github page
* 到該專案的`settings`設定`github pages`點選`launch automatic page generaotr` 一路照預設的點next
* 建立完後會建立 branch 為`gh-pages`，只有在這個branch下的才會在github pages上顯示，網址是https://username.github.io/eric_profile/


### 設定hexo deploy to github
* 修改 `_config.yml` 設定deploy git 資訊

```yml
deploy:
	type: git
	repository: git@github.com:force416/eric_profile.git
	branch: gh-pages
```


### 產生檔案 & deploy

```bash
$ hexo generate
$ hexo deploy
```
