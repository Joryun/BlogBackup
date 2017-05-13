---
title: 玩转Spring Boot之Hello World篇
date: 2016-12-30 21:49:51
categories: "Coding"
tags:
	- spring
	- springboot
	- 框架
---

玩过Spring全家桶的都知道，Spring家族的框架不仅强大，更是项目构建的好帮手。而接下来，将介绍一款Spring家族的框架——Spring Boot.

#### Spring Boot基本概念

由Pivotal团队提供的全新框架，其设计目的是用来简化新Spring应用的初始搭建以及开发过程，并使用“习惯优于配置”的理念让你的项目快速运行起来。使用Spring Boot很容易创建一个独立运行（运行jar，内嵌Servlet容器）、准生产级别的基于Spring框架的项目，使用Spring Boot你可以不用或者只需要很少的Spring配置。


#### Spring Boot 的优点

* 开发者快速入门
* 开箱即用（自带各种默认配置，简化项目配置项）
* 无冗余代码生成和XML配置文件


#### 搭建Spring Boot 的方式

* Eclipse：习惯用Eclipse开发的可使用STS来构建Spring Boot项目
* IntelliJ IDEA：推荐的开发工具，功能强大，使用IDEA可直接新建Spring Boot项目
* Spring Boot CLI：Spring Boot提供的控制台命令工具
* Maven手工构建：构建空的Maven项目，修改pom.xml，增加Spring Boot的依赖包
* http://start.spring.io

#### 接下来通过一个简单的Demo来熟悉下Spring Boot项目的基本构建.

#### 目的

* 构建一个基于Maven的Spring Boot项目,并实现一个简单的Http请求处理
* 了解Spring Boot项目创建,运行过程,项目结构,简单、开发快速的特性

----------

### 创建SpringBoot项目
访问：[http://start.spring.io/](http://start.spring.io/) , 通过SPRING INITIALIZR工具生成基础项目

![](http://upload-images.jianshu.io/upload_images/2929536-2e1c95d2249e5988.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

下载到本地之后，文件夹里的内容如下：

![](http://upload-images.jianshu.io/upload_images/2929536-84265d7f3fe6643b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 导入IDEA
将生成的demo以Maven项目的形式导入IDEA
项目结构如下：

![](http://upload-images.jianshu.io/upload_images/2929536-9265efb37f1bcbd8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 引入Web模块
新建工程的pom.xml,已经引入了2个依赖模块 
分别为：spring-boot-starter（核心模块）  spring-boot-starter-test（测试模块）
接下来需要引入Web模块 : spring-boot-starter-web

![](http://upload-images.jianshu.io/upload_images/2929536-3c464c343b654f48.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

添加spring-boot-starter-web配置后，运行maven->Reimport，更新pom.xml

![](http://upload-images.jianshu.io/upload_images/2929536-967c3fa98fa476dd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

添加完spring-boot-starter-web后,项目支持web注解
基本上有利用SpringMVC开发项目的，很多都接触过注解式开发，而这也是spring的首选开发方式
```
@RestController
RequestMapping("/hello")
```

### 添加HelloWord服务
在默认生成的com.example包下创建一个web文件夹，并新建一个controller，用于输出“Hello World”
```
@RestController
public class HelloController {    
    @RequestMapping("/hello")    
    public String index(){        
        return "Hello World";    
    }
}
```

![](http://upload-images.jianshu.io/upload_images/2929536-f57e7e0b731e7bef.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 启动主程序
点击IDEA右上角的启动服务器图标启动主程序

![](http://upload-images.jianshu.io/upload_images/2929536-1faaaf2c4f1c51fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

打开浏览器访问[http://localhost:8080/hello](http://localhost:8080/hello)，页面输出Hello World
默认启动端口：8080

![](http://upload-images.jianshu.io/upload_images/2929536-4149737ff78d1ff0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


至此，Spring Boot Demo创建完成.
有啥问题可以一起讨论哈！！！