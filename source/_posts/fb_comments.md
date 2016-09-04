---
title: hexo套用fb的comments
date: 2016-04-26 20:06:17
tags:
	- facebook comments
	- hexo
categories: hexo
comments: true
toc: true
description: 如何套用facebook comments的功能
---
### 申請fb開發者應用程式ID
* 上fb的[開發者網站](https://developers.facebook.com/)的官網註冊應用程式網站

### 套用至網站
* 上 [fb embedded comments](https://developers.facebook.com/docs/plugins/embedded-comments) 取得內嵌程式的code
* 貼入`<body />`裡
```javascript
<div id="fb-root"></div>
<script>(function(d, s, id) {
  var js, fjs = d.getElementsByTagName(s)[0];
  if (d.getElementById(id)) return;
  js = d.createElement(s); js.id = id;
  js.src = "//connect.facebook.net/zh_TW/sdk.js#xfbml=1&version=v2.6&appId=8";
  fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));</script>
```

* 貼入想呈現留言區塊的地方
```javascript
<div class="fb-comment-embed" data-href="${抓取目前文章的網址}" data-width="560" data-include-parent="false"></div>
```

### 開始使用
