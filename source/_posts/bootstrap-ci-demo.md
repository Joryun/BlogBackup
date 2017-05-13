---
title: 与Bootstrap和CI框架纠缠的三天
date: 2016-12-31 11:39:35
categories: "Coding"
tags:
	- bootstrap
	- codeigniter
	- php
---


如题，博主为交附个课程设计，只得用三天时间纠缠于不熟悉的领域中...

一直以来，前台都是我的硬伤，否提用bootstrap框架，html5，css，js的简单整合都未必能得心应手，而对于我而言，只单单熟悉后台的业务实现，却无法设计出相映衬的前台UI，这点确实是烦恼已久。刚好，趁这次机会，稍微接触下完全不熟悉的bootstrap框架以及许久没用的CI框架，完成一次基本的整合。当然，实现的功能并不复杂，但若是想试下整合，或者想了解下ci框架处理业务的方式，便可以参考下。

-------------------

系统介绍：此次实现的是一个简单的毕业设计选题管理系统，目前是有学生和教师端，基本都是简单整合，无考虑表单重复提交问题，单点登录问题，sql注入等问题。

学生端功能：
1. 查看个人信息
2. 查看公告
3. 查看可选题目（管理员分配教师，学生仅可查看该教师的课题）
4. 查看已选题目
5. 下载资料页面（不全）

教师端功能：
1. 查看公告
2. 查看可选题目
3. 查看学生列表
4. 上传资料页面（不全）


## Bootstrap框架整合进CI

#### Bootstrap：简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。

#### CI：CodeIgniter 是一个小巧但功能强大的 PHP 框架，作为一个简单而“优雅”的工具包，它可以为开发者们建立功能完善的 Web 应用程序。

单从快速开发来说的话，bootstrap+ci确实是很方便，毕竟都是快速开发，而且很容易上手。但由于博主擅长的是j2ee，因此也不过多解释了。严格意义上来说，这两个框架确实只是会用（当然前提是给看官方文档哈哈）.

### 官网下载ci环境包

下载下来的ci环境包内容如下：
![](http://img.blog.csdn.net/20161229225623292?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSm9yeXVu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### ci框架的基本配置
1. 解压缩安装包

2. 将 CodeIgniter 文件夹及里面的文件上传到服务器，通常 index.php 文件将位于网站的根目录（ps：博主仅为了练手，因此将其部署于本地服务器，即xampp-htdocs）

3. 使用文本编辑器打开 application/config/config.php 文件设置你网站的根 URL
![](http://img.blog.csdn.net/20161229230748496?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSm9yeXVu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

4. 配置数据库参数，打开application/config/database.php
![](http://img.blog.csdn.net/20161229231026060?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSm9yeXVu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### 初步整合
1. 准备好bootstrap demo

2. 将demo的html页面置于ci框架的view层
![](http://img.blog.csdn.net/20161230111919590?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSm9yeXVu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
3. 将js，css，font等资源文件置于_static目录下
![](http://img.blog.csdn.net/20161230112039179?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSm9yeXVu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

4. 修改下主页面css和js的link链接，完成基本的整合


## 系统设计
#### 界面UI
首先，在view层分两文件夹，分别为student和teacher,用于存放各自相应的php文件。

![](http://img.blog.csdn.net/20161230205159288?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSm9yeXVu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### 以学生端为示例
中间的内容显示内嵌了iframe.

![](http://img.blog.csdn.net/20161230205507743?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSm9yeXVu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

##### Choosable页面

![](http://img.blog.csdn.net/20161230211326565?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSm9yeXVu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![](http://img.blog.csdn.net/20161230211410565?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSm9yeXVu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

ps：选题按钮还没添加控制器.

##### Selected页面

![](http://img.blog.csdn.net/20161230211556129?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSm9yeXVu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

ps:留言功能还未完善.

##### Data页面

![](http://img.blog.csdn.net/20161230211727535?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSm9yeXVu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
ps:下载文件功能还未完善.

#####系统基本思路
1. 默认进系统的为Notice页面，即通过控制器load Notice页面.
2. 接着触发Choosable页面，而这过程先是action至该页面的控制器，然后传Choosable所需的数据，并以数组的形式返回，接着在目标页面（即Choosable页面）遍历即可
3. 其余页面的控制思路大同小异，但在form表单action的时候要注意路径问题，一般可调用ci内置的url helper函数获取服务器路径，可避免URL出错

#####注意
1. 务必按照ci的编程规范编写，否则易出bug
2. 加载数据库，使用url helper以及session等功能，记得在构造函数那儿定义好，这样即可在控制器的全局使用
![](http://img.blog.csdn.net/20161230211047278?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSm9yeXVu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### 系统源码
详细的源码可访问博主Github：
https://github.com/Joryun/BiShe.git

#### 系统总结
博主三天捣鼓的简单整合系统，基本上完成了大致的整合以及一些基本功能，由于时间有限，后续的一些基本功能都没加上，但实现的思路都是类似的。这次为了应付课程设计也是拼了，随便捣鼓了这些原本不是很熟悉的东西，但总体来说还是挺好玩的。有兴趣加入更多模块和安全机制或功能的朋友大可以尝试下，博主仅在玩玩儿哈哈~~~

新的一年将至，这个就算一个纪念吧！新的一年，博主会着重游走于Github，强化自身项目经验，做出更好的项目与大家一起交流学习，希望新的一年，程序猿们一起共勉！！






