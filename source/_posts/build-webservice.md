---
title: 新手搭建调用webservice那些坑
date: 2016-05-26 13:40:30
categories: "Coding"
tags:
	- java
	- webservice
	- php

---

今天主要和大家分享搭建java版webservice，以及php调用webservice遇到的一些坑。博客内容大部分纯手打，纯亲测。
注：网上有很多使用Eclipse构建webservice的教程，不过配置较麻烦，而且最后可能还访问不了。因此，此博客采用MyEclipse搭建。需注意一点，MyEclipse10及以下的支持不了pattern库，因此发布的项目如果包含Pattern则无法支持，这也是博主换IDE的原因。

#### 开发环境：MyEclipse2014，JAX-WS构建（容易使用），Tomcat 7


#### 何为WebService？

它是一种构建应用程序的普遍模型,可以在任何支持网络通信的操作系统中实施运行;它是一种新的web应用程序分支，是自包含、自描述、模块化的应用，可以发布、定位、通过web调用。Web Service是一个应用组件,它逻辑性的为其他应用程序提供数据与服务.各应用程序通过网络协议和规定的一些标准数据格式（Http，XML，Soap)来访问Web Service,通过Web Service内部执行得到所需结果.Web Service可以执行从简单的请求到复杂商务处理的任何功能。一旦部署以后，其他Web Service应用程序可以发现并调用它部署的服务。

#### 关键的技术和规则
    
在构建和使用Web Service时,主要用到以下几个关键的技术和规则:

* XML:描述数据的标准方法.
* SOAP:表示信息交换的协议.
* WSDL:Web服务描述语言.
* UDDI:通用描述、发现与集成，它是一种独立于平台的，基于XML语言的用于在互联网上描述商务的协议.

#### **XML**
   

   可扩展的标记语言(XML)是Web service平台中表示数据的基本格式。除了易于建立和易于分析外，XML主要的优点在于它既是平台无关的，又是厂商无关的。无关性是比技术优越性更重要的：软件厂商是不会选择一个由竞争对手所发明的技术的。

#### **SOAP**
 
 
  SOAP是web service的标准通信协议，SOAP为simple object access protocoll的缩写，简单对象访问协议. 它是一种标准化的传输消息的XML消息格式。

#### **WSDL**
  

   WSDL的全称是web service Description Language,是一种基于XML格式的关于web服务的描述语言。其主要目的在于web service的提供者将自己的web服务的所有相关内容,如所提供的服务的传输方式，服务方法接口，接口参数，服务路径等，生成相应的完全文档，发布给使用者。使用者可以通过这个WSDL文档，创建相应的SOAP请求消息，通过HTTP传递给webservice提供者；web服务在完成服务请求后，将SOAP返回消息传回请求者，服务请求者再根据WSDL文档将SOAP返回消息解析成自己能够理解的内容。

#### **UDDI**
  

   将web service进行UDDI注册发布,UDDI是一种创建注册表服务的规范,以便大家将自己的web service进行注册发布供使用者查找.然而当服务提供者想将自己的web service向全世界公布，以便外部找到其服务时，那么服务提供者可以将自己的web service注册到相应的UDDI商用注册网站，目前全球有IBM等4家UDDI商用注册网站。因为WSDL文件中已经给定了web service的地址URI，外部可以直接通过WSDL提供的URI进行相应的web service调用。所以UDDI并不是一个必需的web service组件，服务方完全可以不进行UDDI的注册。

----------

## 开始搭建webservice
#### 前提：首先安装好MyEclipse2014，保证jdk环境配置好了，有tomcat服务器（没有也没关系，MyEclipse自带MyEclipse Tomcat 7，亲测好用，默认端口为8080）。

* 创建发布webservice
* 配置Tomcat 
* 部署项目并启动Tomcat服务器
* 添加JAX-WS库
* 测试webservice

     
 
### 创建发布webservice

#### 新建Web Service Project
![](http://img.blog.csdn.net/20160526144616800)
#### 然后填好信息并next
![](http://img.blog.csdn.net/20160526144930826)
#### 然后接下来一直next，可选择生成web.xml.
#### 这是刚新建的项目结构
![](http://img.blog.csdn.net/20160526145130186)

#### 然后新建一类文件UserInfo.java
![](http://img.blog.csdn.net/20160526145457078)

示例源码：

```
package com.yuan.webservice;
/**
 * 
 * @author Joryun
 *
 */
public class UserInfo {
	public String GetUserInfo(){
		return "源哥";
	}
	
	public String ParameterTest(String user, String pwd){
		return user+"："+pwd;
	}
}

```
#### 接下来发布web service
![](http://img.blog.csdn.net/20160526145727673)
#### 选择从java类创建web service
![](http://img.blog.csdn.net/20160526150314214)
#### 选择访问的java class
![](http://img.blog.csdn.net/20160526150649656)

![](http://img.blog.csdn.net/20160526150700662)
#### 生成WSDL（WSDL以上有介绍，不懂可以回去看）
![](http://img.blog.csdn.net/20160526150713032)
#### 发布后的项目结构如下
![](http://img.blog.csdn.net/20160526151228211)


### 配置Tomcat
#### 假定你需要使用自己本机Tomcat的情况下，教程如下：
#### Window-Preferences-MyEclipse-Servers-Tomcat
![](http://img.blog.csdn.net/20160526151910516)

![](http://img.blog.csdn.net/20160526152006074)
#### 配置好后Apply-OK.



### 部署项目并启动Tomcat服务器

#### 部署此项目到服务器
![](http://img.blog.csdn.net/20160526152648665)

![](http://img.blog.csdn.net/20160526152701654)

![](http://img.blog.csdn.net/20160526152710686)
#### 选择完后Finish
#### 接下来启动Tomcat服务器
![](http://img.blog.csdn.net/20160526153044203)
#### 服务器已启动的图例
![](http://img.blog.csdn.net/20160526153052937)


### 添加JAX-WS库

#### 在项目的构建路径中添加库文件
![](http://img.blog.csdn.net/20160526153640221)

![](http://img.blog.csdn.net/20160526153659648)

![](http://img.blog.csdn.net/20160526153815525)

![](http://img.blog.csdn.net/20160526153842572)

### 测试webservice

#### 输入URL，出现图式效果即为发布成功.
```
URL : http://localhost:8080/WebServiceDemo/UserInfoPort?wsdl
```

![](http://img.blog.csdn.net/20160526154324689)


----------

## PHP调用webservice
#### 注：博主采用CI框架测试，但不用框架也一样。并且php项目文件发布到了xampp上，直接访问本地即可查看效果。
#### 关于php调用webservice，亲测过两种方法：

#### **1. 引入nusoap.php，调用call()方法**
#### 特别注意：以下两处圈红圈的是坑点，一开始测试的时候用的是webservice接口名的参数，即user，pwd.但实际上打印到网页上之后才发现参数是arg0和arg1。。。
![](http://img.blog.csdn.net/20160526155851882)

![](http://img.blog.csdn.net/20160526160147935)
 

 
#### **2. php5自带函数测试，classMap方式传值**    

![](http://img.blog.csdn.net/20160526160403623)

#### 以下贴PHP实现源码：

```
<?php
header('Content-Type: text/html; charset=UTF-8');
/**
 * Class Test
 * Joryun
 *
 * 调用webservice测试类
 */
class Test extends CI_Controller
{
    public function __construct()
    {
        parent::__construct();
    }

    public function index()
    {
        /**
         * nusoap.php需在网上下载，并将该php文件包含进项目空间
         * 引入nusoap.php，调用call()方法
         */
//        require_once ("libs/nusoap.php");
//
//        // Create the client instance
//        $client = new nusoap_client('http://localhost:8080/WeixinDemo/UserInfoPort?wsdl', true);
//        $client->soap_defencoding = 'utf-8';
//        $client->decode_utf8 = false;
//        $client->xml_encoding = 'utf-8';
//
//        $param = array('arg0'=>'Joryun', 'arg1'=>'666666');//webservice参数数组
//        $result = $client->call('ParameterTest', $param);//接口和参数
//        print_r($result);



        /**
         * php5自带函数测试
         * classMap方式传值
         */
        $client = new SoapClient("http://localhost:8080/WeixinDemo/UserInfoPort?wsdl");

        echo ("SOAP服务器提供的开放Function:");
        echo '<pre>';
        var_dump ( $client->__getFunctions () );//获取服务器上提供的方法
        echo '</pre>';

        echo '<br>';

        echo ("SOAP服务器提供的Type:");
        echo '<pre>';
        var_dump ( $client->__getTypes () );//获取服务器上数据类型
        echo '</pre>';

        $object=new stdclass;
        $object->arg0='Joryun';
        $object->arg1='666666';
        $result = $client->ParameterTest($object);
        //$result=get_object_vars($result);   //将object转换为array
        var_dump($result);
    }
}

?>
```

#### 好了，今天的教程就说到这里了<(￣︶￣)>
#### 当然了，之所以想分享是因为其中是有一些坑在，搞了一天多才搞定了。欢迎大家交流，有啥指导直说无妨哈哈哈哈~~