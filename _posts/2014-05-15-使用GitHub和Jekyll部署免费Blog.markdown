---
layout: post
title:  "使用GitHub和Jekyll部署免费Blog"
date:   2014-05-15 22:30:42
categories: jekyll update
---

懒得折腾WordPress，只想好好静下心来记录一些文字。所以[GitHub](http://Github.com)配上[Jekyll](http://jekyllrb.com/)便是我的首选了，免费还有版本控制功能加上简洁的Markdown编辑语言何乐而不为呢，废话不多，开搞！

__注意：本教程全程在Mac上操作，并且默认你已经了解了Git和GitHub的基本知识，并已经拥有GitHub账号，对于以上知识不了解的朋友请Google。__

## Jekyll
1.安装jekyll，在控制台内输入下面得命令即可完成安装。

__gem install jekyll__

2.创建本地网站文件，同样在控制台内输入以下命令即可生成Jekyll默认网站文件。

__jekyll new testblog__


3.在本地预览网站，在控制台内输入下面的命令后，Jekyll变在后台开启了一个小型的web服务器，我们只要在浏览器内输入http://localhost:4000 即可访问网站

__cd testblog__

__jekyll server__

![create_jekyll_blog](http://wellsnakeblog.qiniudn.com/2014051501create_jekyll_blog.png)

4.最后我们需要创建本地版本库用来上传至Github，进入网站文件夹后输入以下命令即可生成一个本地的Git版本库。

__git init__

![gitinit](http://wellsnakeblog.qiniudn.com/2014051501gitinit.png)


## GitHub
1.创建新的版本库，名称为username.github.io,其中 __username__ 是你GitHub得账号名，然后会获得一个版本库地址。创建完后会获得一个Git版本库的地址，先记下来后面有用。

![create_new_repository](http://wellsnakeblog.qiniudn.com/2014051501create_new_repository.png)

![repository_url](http://wellsnakeblog.qiniudn.com/2014051501repository_url.png)

2.对于Git不熟悉的朋友可以使用[SourceTree](http://www.sourcetreeapp.com/)这个免费又好用的Git管理工具来管理你的Git版本库，绝对是命令行苦手的福音啊。

![SourceTree](http://wellsnakeblog.qiniudn.com/2014051501SourceTree.png)

3.在控制台内输入以下命令可以将刚才我们创建的blog文件加入并提交至Git版本库。

__git add -A__

__git commit -m "first commit"__

4.在控制台内输入以下命令将刚才在GitHub的版本库地址加入到本地的版本库内，然后将本地版本库变动上传到GitHub上，过程中需要输入你在GitHub的账号和密码。等上传完后就是见证奇迹的时刻了。

__git remote add origin https://github.com/wellsnake/test.github.io.git__

__git push -u origin master__

![push_to_github](http://wellsnakeblog.qiniudn.com/2014051501push_to_github.png)

6.使用 http://test.github.io 这个网址访问我们的网站吧！呵呵奇迹没有发生只有404页面。从页面中我们可以了解到完成提交后GitHub Pages大约会在10分钟后才会有反应，那就去泡杯咖啡看看电视再回来吧。
![github_404](http://wellsnakeblog.qiniudn.com/2014051501github_404.png)


## 绑定域名
其实到前面一步我们已经完成了整个Blog的部署了。除了使用默认地址来访问我们的网站外，我们还可以绑定域名。（这个功能实在是太棒了！）

1.进入本地网站文件加后创建名为 __CNAME__ 的文件，然后输入你的域名（下图中为wellsnake.com）然后保存即可。最后commit本地文件修改并上传到GitHub上即可。这里大家会发现为什么我在本地目录里有_site文件夹而上传到GitHub上却没有了呢，打开.gitignore（隐藏文件）文件后聪明的朋友应该明白怎么回事了吧。

![edit_cname](http://wellsnakeblog.qiniudn.com/2014051501edit_cname.png)

2.最后我们到自己的域名管理系统内设置IP地址指向即可。（本处使用的是DNSPod的域名管理系统）等个一会后应该就能使用自己的域名来反问网站了！

![dns_config](http://wellsnakeblog.qiniudn.com/2014051501dns_config.png)

好啦，至此整个部署的工作已经全部完成，至于后面关于如何发布文章和加入评论功能就下一篇再发布吧。今天就写到这里！


