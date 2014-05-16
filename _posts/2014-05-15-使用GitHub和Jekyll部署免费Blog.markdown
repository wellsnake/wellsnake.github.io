---
layout: post
title:  "使用GitHub和Jekyll部署免费Blog"
date:   2014-05-15 22:30:42
categories: jekyll update
---

懒得折腾WordPress，只想好好静下心来记录一些文字。所以[GitHub](http://github.com)配上[Jekyll](http://jekyllrb.com/)便是我的首选了，免费还有版本控制功能何乐而不为呢，废话不多，开搞！

## Jekyll
1.安装jekyll，在控制台内输入下面得命令即可完成安装。

**gem install jekyll**

2.创建本地网站文件，同样在控制台内输入以下命令即可生成Jekyll默认网站文件。

**jekyll wellsnakeblog**


3.在本地预览网站，在控制台内输入下面的命令后，Jekyll变在后台开启了一个小型的web服务器，我们只要在浏览器内输入http://localhost:4000 即可访问网站

**cd wellsnakeblog**

**jekyll server**

![setupjekyll](http://ww4.sinaimg.cn/large/7dc1089egw1egfas5vnbsj20fp05oab5.jpg)

4.最后我们需要创建本地版本库用来上传至Github，进入网站文件夹后输入以下命令即可生成一个本地的git版本库。

**git init**

![gitinit](http://ww4.sinaimg.cn/large/7dc1089egw1egfas4xmw2j20fu01wdfz.jpg)


## GitHub
1.创建新的版本库，名称为username.github.io,其中**username**是你GitHub得账号名，然后会获得一个版本库地址。创建完后会获得一个git版本库的地址，先记下来后面有用。

![prositiory](http://ww2.sinaimg.cn/large/7dc1089ejw9egftqx9gldj20id0d5gnd.jpg)

![prositioryurl](http://ww3.sinaimg.cn/large/7dc1089egw1egfas15skgj20kb046aak.jpg)

2.对于git不熟悉的朋友可以使用[SourceTree](http://www.sourcetreeapp.com/)这个免费又好用的git管理工具来管理网站得版本库。

3.安装完SourceTree后选择**Create Repository**，**Destination Path**选择刚才创建的本地网站文件夹。这样就可以该软件来管理我们刚才创建的本地版本库了，绝对是命令行苦手的福音啊。

![addprositiory](http://ww2.sinaimg.cn/large/7dc1089ejw9egfd9pbtycj20ho08q75q.jpg)

4.进入版本库内后选择**Settings**，将刚才在GitHub上创建的版本库地址填入**URL**内，这样就将本地版本库与GitHub上的版本库绑定了。

![settingremout](http://ww2.sinaimg.cn/large/7dc1089ejw9egftmlgsxsj20i90ca76v.jpg)

5.commit本地文件内容变更，最后点击**Push**将本地版本库更新到GitHub上，然后就是见证奇迹的时刻了。

![commitandpull](http://ww3.sinaimg.cn/large/7dc1089ejw9egftq6l61nj20m20k5n1d.jpg)

6.使用 http://wellsnake.github.io 这个网址访问我们得网站吧！呵呵奇迹没有发生只有404页面，因为第一次提交后GitHub大约会在10分钟后才会有反应，那就去泡杯咖啡看看电视再回来吧。
![web404](http://ww1.sinaimg.cn/large/7dc1089egw1egfarnnh80j20ii0c1t99.jpg)
![10minutes](http://ww1.sinaimg.cn/large/7dc1089egw1egfaro47ggj20j803bt8u.jpg)


## 绑定域名
其实到前面一步我们已经完成了整个Blog的部署了。除了使用默认地址来访问我们的网站外，我们还可以绑定域名。（这个功能实在是太棒了！）

1.进入本地网站文件加后创建名为**CNAME**的文件，然后输入你的域名（下图中为wellsnake.com）然后保存即可。最后commit本地文件修改并push到GitHub上即可。

![addcname](http://ww4.sinaimg.cn/large/7dc1089egw1egfdv9mtd4j20dd06z0u0.jpg)

2.最后我们到自己得域名管理系统内设置IP地址指向即可。（本处使用的是DNSPod的域名管理系统）等个一会后应该就能使用自己的域名来反问网站了！
![dnspod](http://ww1.sinaimg.cn/large/7dc1089egw1egfe325ltqj20gq03gjrg.jpg)

好啦，至此整个部署的工作已经全部完成，至于后面关于如何发布文章和加入评论功能就下一篇再发布吧。今天就写到这里！


