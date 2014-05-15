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

