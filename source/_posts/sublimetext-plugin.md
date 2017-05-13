---
title: Sublime Text 3(Mac版)常用插件篇
date: 2017-02-05 16:57:40
categories: "Coding"
tags:
	- mac
	- 编辑器
	- 插件
---

以下大部份插件Windows安装方法基本与Mac类似.
首先，Sublime Text无疑是编程中一款强有力的工具，深受程序猿的喜爱，下面简单介绍下Sublime Text.

### Sublime Text
一款具有代码高亮、语法提示、自动完成且反应快速的编辑器软件，不仅具有华丽的界面，还支持插件扩展机制，用它来写代码，绝对是一种享受。

接下来直接切入主题，安装过程并不重要，旨在于提高编程效率，因此不会列出众多方法，实在没那个必要.
文章的最后提供Sublime Text 3(Mac版)破解版，可直接使用，若链接失效，可私聊.

#### 安装Package Control
首先通过快捷键 ctrl+` (~)或者 View > Show Console 打开控制台(注：安装有QQ输入法的这个快捷键会有冲突的，输入法属性设置-输入法管理-取消热键切换至QQ拼音)，输入以下代码，enter即可.

```
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```

#### 使用Package Control组件安装插件
Cmd+Shift+P（菜单 – Tools – Command Paletter，Windows快捷键：Ctrl+Shift+P），输入 install 选中Install Package并回车，输入或选择你需要的插件回车就安装了（注意左下角的小文字变化，会提示安装成功），安装其它插件也类似.

![](http://upload-images.jianshu.io/upload_images/2929536-b225e9401d781431.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![](http://upload-images.jianshu.io/upload_images/2929536-74525aee8b1e4988.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 常用插件推荐
* Emmet
——Emmet 官方提供的 Sublime Text 扩展；//即zencoding，写html先装这一个就够了
* SublimeLinter
——代码校验插件，支持 HTML、CSS、JS、PHP、Java、C++ 等16种语言；
* HTML5
* Alignment
——代码对齐插件
* jQuery
——代码智能提示插件
-Git
—整合 Git 功能的插件
* LESS
——LESS 代码高亮插件
* JsFormat
——JavaScript 代码格式化插件
* LiveReload
——让页面即时刷新
* Pretty JSON
——JSON美化扩展
* Can I Use
——查询 CSS 属性兼容情况
* CoffeeScript
——CoffeeScript 代码高亮，校验和编译等
* ColorPicker
——跨平台取色器插件

#### Sublime Text 3(Mac版)
百度网盘
URL：https://pan.baidu.com/s/1slW5AUD
Password:  rpsu

#### 总结
插件可以根据开发类型选择性装特定的插件，毕竟Sublime Text只有拓展插件才能更加优雅地编程。此外，还需要熟记大部份常用的快捷键，才能大大提高编程效率。
此文章隶属于教程篇，不足肯定是有的，但只要有钻研精神，相信大家可以在编程路上吸取更多经验。共勉之！！！