---
title: vue.js + vue-router + webpack
toc: true
comments: true
date: 2017-05-09 09:00:59
description: vuejs建構前端專案練習
tags: 
    - vue.js
    - vue-router
    - webpack
categories:
    - vue.js
---
前陣子有機會接觸到 `vue.js` 這套 js framework 就著手進行練習，練習的內容放置上 [github vue-practice](https://github.com/force416/vue-practice)，並且透過 [github page](https://force416.github.io/vue-practice/) Demo

### npm dependencies

```json

//package.json

{
  "name": "vue-practice",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "dev": "cross-env NODE_ENV=development webpack-dev-server --inline --progress --port 3000 --content-base ./",
    "build": "cross-env NODE_ENV=production webpack --progress --hide-modules"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "vue": "^2.3.2",
    "vue-router": "^2.5.3"
  },
  "devDependencies": {
    "babel-core": "^6.0.0",
    "babel-loader": "^6.0.0",
    "babel-preset-es2015": "^6.24.1",
    "babel-preset-latest": "^6.0.0",
    "cross-env": "^3.0.0",
    "css-loader": "^0.25.0",
    "file-loader": "^0.9.0",
    "vue-loader": "^11.1.4",
    "vue-template-compiler": "^2.2.1",
    "webpack": "^2.2.0",
    "webpack-dev-server": "^2.2.0"
  }
}

```

`dependencies` 主要是`vue`、`vue-router`，而`devDependencies`的部份主要是
* `babel-loader` - `webpack`的loader，主要負責將`es2015`的語法轉成`es5`
* `vue-loader` - 讓`webpack`可以認得`.vue`檔案，並加以打包
* `webpack` - 最主要的打包工具
* `webpack-dev-server` - 提供開發模式的輕量server

```json
"scripts": {
    "dev": "cross-env NODE_ENV=development webpack-dev-server --inline --progress --port 3000 --content-base ./",
    "build": "cross-env NODE_ENV=production webpack --progress --hide-modules"
  }
```
在執行的指令設定`dev`、`build`，可以透過`npm`指令執行

``` shell
$npm run dev //啟動webpack-dev-server方便開發

$npm run build //打包成production環境的js
```

### webpack

``` javascript

//webpack.config.js

var path = require('path')
var webpack = require('webpack')

module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, './dist'),
    publicPath: '/dist/',
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader',
        options: {
          loaders: {
          }
          // other vue-loader options go here
        }
      },
      {
        test: /\.js$/,
        loader: 'babel-loader',
        exclude: /node_modules/,
        query: {
          presets: ['es2015']
        }
      },
      {
        test: /\.(png|jpg|gif|svg)$/,
        loader: 'file-loader',
        options: {
          name: '[name].[ext]?[hash]'
        }
      }
    ]
  },
  resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    }
  },
  devServer: {
    historyApiFallback: true,
    noInfo: true
  },
  performance: {
    hints: false
  },
  devtool: '#eval-source-map'
}

if (process.env.NODE_ENV === 'production') {
  module.exports.devtool = '#source-map'
  // http://vue-loader.vuejs.org/en/workflow/production.html
  module.exports.plugins = (module.exports.plugins || []).concat([
    new webpack.DefinePlugin({
      'process.env': {
        NODE_ENV: '"production"'
      }
    }),
    new webpack.optimize.UglifyJsPlugin({
      sourceMap: true,
      compress: {
        warnings: false
      }
    }),
    new webpack.LoaderOptionsPlugin({
      minimize: true
    })
  ])
}

```

`webpack.config.js`預設放在根目錄下，`webpack`會自動解析裡面的設定，`entry`是設定`webpack`在打包程式時的進入點，`output`是打包完成後的程式輸入設定，包括檔名、目錄，這裡設定的是輸入到路徑 `/dist/bundle.js`。

透過`webpack`提供的plugin `UglifyJsPlugin`、`LoaderOptionsPlugin`可以將打包出來的js檔案進行uglify & minify

### vue-router

``` javascript

//router.js

import Vue from 'vue'
import VueRouter from 'vue-router'
import DashboardComponent from '../component/dashboardComponent.vue'
import ProfileComponent from '../component/profileComponent.vue'

Vue.use(VueRouter)

const routes = [
    { path: '/dashboard/:userId', name: 'dashboard', component: DashboardComponent },
    { path: '/profile', name: 'profile', component: ProfileComponent }
]

var vueRouter = new VueRouter({
    base: 'vue-practice',
    // mode: 'history',
    routes: routes
});

export default vueRouter

```

這裡要注意

    mode: 'history'
 
 如果將`mode`設定為history代表要啟用html5 history api，vue-router產生出來的url就會像一般的url一樣 `http://yoursite.tw/post/first`，反之如果沒有設定的話產生出來的url就會帶有`#`的hash值url `http://yoursite.io/#/dashboard/123`

    Vue.use(VueRouter)

使用模組化的方式寫`vue.js`時，導入 `vue-router` 需要呼叫 `Vue.use(VueRouter)`

### index.html

``` html

//index.html

<body>
    <div id="app" />
</body>
<script src="dist/bundle.js"></script>

```

在`vue.js`的入口只需要引用打包完成後的`bundle.js`，在正式 production 環境時可以減少http request js的數量，`vue.js`也會自動處理各component的相依問題。

### reference

以上資訊參考至

[vue.js](https://vuejs.org/)
[vue-router](https://router.vuejs.org/)
[webpack](https://webpack.js.org/)