---
title: 提高Github Clone速度
date: 2017-02-27 21:57:27
categories: "Coding"
tags:
	- github
	- git
---

以下操作均在mac下，当然，windows也类似。
如题。使用git clone速度之慢，简直绝了。因此，在这里将提出一种较为简单的解决方法，有兴趣花丢丢时间折腾的朋友可以试试。

虽说git clone跟网速离不了干系（有些地区较快，有些地区较慢），但总体来说，大部分都在10KiB/s-20KiB/s之间，及其慢。若是需要clone大repo，那速度简直捉急。

下面简单说下解决方案：
1.用 git 内置代理，直接走系统中运行的代理工具中转，比如，你的 SS 本地端口是 1080（一般port均为1080），那么可以如下方式走代理：

```
git config --global http.proxy socks5://127.0.0.1:1080
git config --global https.proxy socks5://127.0.0.1:1080
```

#### 具体步骤如下：
编辑.gitconfig文件

![](http://upload-images.jianshu.io/upload_images/2929536-a7f7b544c5a7bd2a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 Enter之后进入vim，按i进行insert

![](http://upload-images.jianshu.io/upload_images/2929536-d3c0ee4dc2458ab2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

按Esc退出，输入:wq保存

![](http://upload-images.jianshu.io/upload_images/2929536-9d55728b6ce9727a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


2.此外，git clone或者git push特别慢，并不是因为[http://github.com](//link.zhihu.com/?target=http%3A//github.com)的这个域名被限制了。而是"[http://github.global.ssl.fastly.Net](//link.zhihu.com/?target=http%3A//github.global.ssl.fastly.Net)"这个域名被限制了。那么可以在hosts文件里进行绑定映射。

####具体步骤如下：
在terminal输入命令并输入开机密码，Enter确认

```
sudo vi /etc/hosts
```

![](http://upload-images.jianshu.io/upload_images/2929536-2ce00e80a7acc931.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 然后依旧在vim上编辑，命令如下
 
```
151.101.72.249 http://global-ssl.fastly.Net
192.30.253.112 http://github.com
```

![](http://upload-images.jianshu.io/upload_images/2929536-0e21c4563955dc87.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

保存之后就可以了。

接下来，你可以在clone一次，ssh或https协议都行，速度翻了好几倍！！！

以下正是亲测的结果，速度已经到达了200多KiB/s！！！
![](http://upload-images.jianshu.io/upload_images/2929536-3a6d1c8f13abf48c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

总结：虽说是细节部分，但是随手优化，不仅能接触更多新奇的东西，还能提高效率，何乐而不为呢...
