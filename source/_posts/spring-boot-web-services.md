---
title: spring boot 建立 web service
toc: true
comments: true
date: 2016-05-28 20:47:08
description: 透過spring boot 快速打造restful web service
tags:
    - web service
categories:
    - spring boot
---
### spring boot 介紹
* [spring boot 官網](http://projects.spring.io/spring-boot/) Spring Boot主要目的就是為了節省配置專案的時間，可以利用他快速建立一個基於RESTful的Web專案

### 建立maven project
* 首先先建立一個一般的maven專案

### pom.xml配置
* 打開 `pom.xml` 加入spring boot 必要引入的lib
``` xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.3.5.RELEASE</version>
</parent>
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```
### 建立spring init class
* 在classpath下建立spring boot 起始，新增檔案`SpringBootSconfiguration.java`內容如下
``` java
@SpringBootApplication
public class SpringBootSconfiguration {
    public static void main(String[] args) {
        SpringApplication.run(SpringBootSconfiguration.class, args);
    }
}
```

### 建立restful web service
* 建立`App.java`，內容如下
```java
@RestController()
@RequestMapping("/z")
public class App
{
    @RequestMapping("/hello/{num}")
    public @ResponseBody Map sayHello(@RequestParam(value="name", required=false, defaultValue="Stranger") String name,@PathVariable int num) {
    	Map<String, Object> resultMap = new HashMap<String, Object>();
    	resultMap.put("name", name);
    	resultMap.put("num", num);
    	resultMap.put("big_penis", "eric");
    	return resultMap;
    }
}
```
* `@RestController` 作用為宣告這class 為 restful風格的controller
* `@RequestMapping("/z")` 為對應的path

### deploy to server
* 由於spring boot已內建tomcat server 故只要以一般執行java class 的方式執行`App.java`即可
* 透過browser連結 `localhost:8080/z/hello/3` 如有回傳json格式資料，即代表成功。

### application.properties
* 如果想要改變預設的 port `8080`，只需要在`src/main/resources`路徑下加入檔案`application.properties` 內容如下
``` properties
server.port = 8090
```
* 加入此設定再重啟spring boot 就可透過browser連結 `localhost:8090/z/hello/3`

### project tree
* [gihub spring boot demo](https://github.com/force416/springboot_demo)
* 專案結構
``` txt
├── pom.xml
├── README.md
├── src
│   └── main
│       ├── java
│       │   └── eric
│       │       └── ws
│       │           ├── App.java
│       │           └── SpringBootSconfiguration.java
│       └── resources
│           └── application.properties
└── target
```
