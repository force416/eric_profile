---
title: Webpack 介紹與使用
toc: true
comments: true
date: 2017-05-04 21:35:49
description:
tags: 
 - webpack
 - npm
 - commonjs
 - amd
categories: webpack
---
Webpack 一開始是基於幫助 `React` 開發和模組管理的工具，也是目前功能最為强大的前端模組管理和打包工具，不只適用於 ReatJs，愈來愈多前端專案也是透過webpack進行打包與管理，使用這個工具前最好先暸解 `CommonJS` 與 `AMD` 關於JavaScript的兩大模組管理規範，

## CommonJS
    
`CommonJS` 是定義模組的同步加載，`Node.JS`就是符合 `CommonJS`，透過`require`關鍵字去引用相關模組

```javaScript
var path = require('path');
var http = require('http');

http.createServer((req, res) => {
    res.statusCode = 200;
});

```
## AMD

`AMD` 是定義模組非同步加載，`RequireJS`就是基於`AMD`的規範，

```javaScript
//定義模組 test.js
define(['math'], function(math){
    function foo() {
        math.doSomething();
    }
    return {
        foo : foo
    }
});


//引用模組
requirejs(['test'], function( test ) {
    console.log( test.foo() );
    //do something
});
```
## NPM

全名是 Node Package Manager，原本目的是`node.js`管理工具，隨著`npm`成為主流的 `JavaScript` 套件發佈平台，很多前端專案都依賴於 `npm` 上的套件，或者透過`npm`發佈套件，透過 `webpack`可以直接在前端的程式碼中直接引用`npm`的套件。

## Webpack

`webpack`的定位可以用官網提供的這張圖解釋

{% asset_img what-is-webpack.png %}

管理一切的靜態資源將 JavaScript 的模組相依做管理與 production 的 minify 與 uglify。

## github webpack-demo

在 [github](https://github.com/force416/webpack-practice/tree/master) 放上webpack練習 project

主要重點是`webpack.config.js`的配置如下

```javascript
var path = require('path');

module.exports = {
    entry: "./js/index.js",
    output: {
        path: __dirname + "/dist",
        filename: 'bundle.js'
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /(node_modules|bower_components)/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: ['es2015']
                    }
                }
            },
            {
                test: /\.css$/, loader: 'style-loader!css-loader'
            }
        ]
    },
    devtool: 'source-map'
}
```

### entry

webpack打包代碼的主要進入點

### output

定義打包完成的 `bundle.js` 要存放的路徑，這裡設定的是存放在`dist`目錄底下

### module.rules

主要是放入 `webpack` 的 `loder`，將符合正規表達式的檔案內容的程式碼做處理，這裡放的是`babel-loader`主要是將`es2015`的代碼轉換成各browser都看得懂的`es5`，在開發上就不必顧慮寫的程式碼是`es2015`、`es2017`，透過 `babel-loader` 輕鬆做轉換。

webpack的loder包含各式各樣程式碼的預處理像是
* `jsx-loader` //jsx
* `coffee-loader` //coffee.script
* `typescript-loader` //typescript
* `style-loader` //處理css
* 其它...
