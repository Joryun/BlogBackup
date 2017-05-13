---
title: webservice(1)：体验查询号码归属地demo
date: 2017-04-15 21:48:04
categories: "Coding"
tags:
	- webservice
	- java
---

对于webservice的介绍，本文就不再赘余讲述。
详见文章 [新手搭建调用webservice那些坑][1]

首先，先给出一个站点，该站点提供了许多webservice服务，可供调用测试。
站点：http://www.webxml.com.cn/zh_cn/index.aspx

![](http://upload-images.jianshu.io/upload_images/2929536-af65f5ffb80d2fc0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如上图所示，我们本文将测试归属地webservice。
我们先查询该webservice相关服务。

![](http://upload-images.jianshu.io/upload_images/2929536-9af27cda29ec84f2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/2929536-32812af9e617e56c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

大家可以在该文本框中输入手机号，userID忽略，点击调用即可查询手机归属地。
接下来我们通过代码测试该ws。

注：请求方式有很多种，分别为post、get、soap、wsimport。在这里，使用wsimport方式请求！！！

## 步骤：
1. 记录所调用webservice的WSDL（每个webservice都会有一个WSDL，WSDL即WebService Description Language – Web服务描述语言）

2. 使用JDK目录下的工具-wsimport，生成调用webservice相应的代码

3. 编写测试类测试


#### 1.记录所调用webservice的WSDL
进入之前的站点，找到相应webservice，点击服务说明


![](http://upload-images.jianshu.io/upload_images/2929536-1da007cd96f3c75e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

以下即为相应WSDL，一份xml文档

![](http://upload-images.jianshu.io/upload_images/2929536-44fab3a2cf49aab2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

copy该站点的URL，如下

```
http://ws.webxml.com.cn/WebServices/MobileCodeWS.asmx?WSDL
```

#### 2.使用JDK目录下的工具-wsimport，生成调用webservice相应的代码

wsimport是一个命令，jdk1.6及以上才可以使用，ws针对不同的语言都会有个wsimport命令，我们可以在自己安装的jdk的bin目录下找到这个wsimport.exe，正因为有了这个，所以我们可以在命令行中使用wsimport命令。
输入以下命令，会在特定的包中生成java与class文件，接着将其copy至项目路径下即可。

```
wsimport -s . -p ws.client.c http://ws.webxml.com.cn/WebServices/MobileCodeWS.asmx?WSDL
```


Problem：在mac下的终端，若使用到了zsh，可能会出现以下情况。

![](http://upload-images.jianshu.io/upload_images/2929536-1a6ca77b85376765.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这是由于zsh不兼容的问题！！！
具体原因：
因为zsh缺省情况下始终自己解释这个 *.h，而不会传递给 find 来解释。
解决方案：
打开terminal，在~/.zshrc中加入: 
setopt no_nomatch, 然后进行source .zshrc命令即可

以下为copy入项目空间的示例图
注：ws.client.test下的WebserviceTest为webservice测试类，暂时忽略。


![](http://upload-images.jianshu.io/upload_images/2929536-203d30b3fd49012a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样就有了号码归属地查询这个ws服务相关的API了，且是通过官方的WSDL来生成的。接着，便是编写测试类测试功能了。

#### 3.编写测试类测试

```
package ws.client.test;
import ws.client.c.MobileCodeWS;
import ws.client.c.MobileCodeWSSoap;

public class WebserviceTest {
	public static void main(String[] args) {

		//获取一个webservice服务
		MobileCodeWS ws = new MobileCodeWS();	

		//获取具体服务类型：get post soap1.1 and soap1.2
		MobileCodeWSSoap wsSoap = ws.getMobileCodeWSSoap();
		String address = wsSoap.getMobileCodeInfo("你的手机号码", null);
		
		System.out.println("手机归属地信息："+ address);
	}
}
```

测试结果示例

![](http://upload-images.jianshu.io/upload_images/2929536-590d9b117d0bda5e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

OK！！！到这里我们就体验完了该webservice。

总结：
webservice中WSDL很重要，里面用xml描述了webservice的信息，所以我们可以通过解析WSDL来获取该webservice相关的API，然后在自己的项目中调用这些API即可调用该webservice。


---------

[1]: http://joryun.com/2016/05/26/build-webservice/