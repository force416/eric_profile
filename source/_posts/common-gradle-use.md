---
title: gradle 基本使用
toc: true
comments: true
date: 2016-05-12 18:38:20
description:
tags:
    - gradle
    - java
categories: java
---
### gradle 簡介
* gradle 相對於 maven 也是一套 java project 的build tool，跟 maven 一樣都是套件管理工具

### 整合Eclipse使用
* 下載gradle 套件 `Gradle IDE Pack`
* 建立`java project` or `dynamic web project`
* 在project 的 root path 下建立 `build.gradle` file
* `build.gradle` 簡易範例內容如下

```gradle
apply plugin: 'java'
apply plugin: 'eclipse'

sourceCompatibility = 1.5
version = '1.0'
jar {
    manifest {
        attributes 'Implementation-Title': 'Gradle Quickstart',
                   'Implementation-Version': version
    }
}

repositories {
    mavenCentral()
}

dependencies {
compile group:'commons-collections',name:'commons-collections',version:'3.2'
testCompile group: 'junit', name: 'junit', version: '4.+'
}

test {
    systemProperties 'property': 'value'
}

uploadArchives {
    repositories {
       flatDir {
           dirs 'repos'
       }
    }
}
```
### 常用gradle task

* `gradle -u tasks` 列出目前有哪些task
* `gradle -u dependencies` 列出套件的相依關係

### 相關參考資源
[spring io](https://spring.io/guides/gs/gradle/)
[CodeData](http://www.codedata.com.tw/java/understanding-gradle-1-ant/)
(http://www.journaldev.com/8118/java-simple-example-with-gradle-eclipse-plugin)
