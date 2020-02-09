---
title: "Jekyll使用篇 1 - 发布文章、加入评论功能、加入Google Analytics"
date: 2014-05-24 20:40:42
categories: jekyll
tags: Jekyll Google Analytics Disqus
key: A-2014-05-24-20-40-42
author: wellsnake
---

## 1.撰写文章
1.Jekyll中一篇文章就是一个文件，所有需要发布的文章都要放在```_posts```文件夹内。Jekyll对于文章的文件名也是有要求的，系统会根据文件名来生成每篇文章的链接地址。具体的格式为：```YYYY-MM-DD-文章标题.markdown``` 其中```YYYY```为4位年份，```MM```是两位的月份，```DD```是两位的日期。下图是本blog的文件列表：

![filelist](http://lc-4REXSuuT.cn-e1.lcfile.com/d0fc89504e434d3a8b632f03edfc6cd6.png)

2.在使用Markdown撰写文章之前我们需要先设置头信息。头信息需要根据[YAML](http://yaml.org/)的格式写在两行三虚线之间。在头信息可以设置预定义的全局变量的值，Jekyll会根据变量的值来生成文章页面。下图是本篇文章的头信息：

![frontmatter](http://lc-4REXSuuT.cn-e1.lcfile.com/81fbf9c0b6014a74ad835264ac27b233.png)

```layout```使用指定的模版文件，不加扩展名。模版文件放在_layouts目录下。

```title```文章的标题。

```date```发布文章的时间。

```categories```将文章设置成不同的属性。系统在生成页面时会根据多个属性值来生成文章地址。以上设置会生```http://.../jekyll/update/...```格式的文章链接。

```tags```标签，一篇文章可以设置多个标签，使用空格分割。

基本上一篇文章只要用到以上一些信息就可以了，当然还有其它的变量可以设置，具体用法可以在[Jekyll网站](http://jekyllrb.com/docs/frontmatter/)上查看。

3.Jekyll是支持图片和其它资源文件的，但本人在此强烈建议所有的文件资源全都通过外链的方式解决，毕竟GitHub主要还是用来管理源代码不适合存放资源文件。如果只是需要简单的图床的话直接使用weibo的私人相册的功能即可就是管理起来不太方便。当然其实最好还是使用像某牛云存储之类的云存储服务，访问量不大的话免费账户基本能满足要求了，管理资源文件也很方便（感觉有点做广告的嫌疑-_-!）。本blog的所有图片就部署在上面，资源的访问速度也很快。

![qiniu](http://lc-4REXSuuT.cn-e1.lcfile.com/65b33504eae94f3ebf45e5afb943db5e.png)

4.前期工作还真多啊，接下来终于可以开始撰写文章啦。写文章的话只要简单的学一下Markdown的语法就可以了。具体语法在此不展开，不会的可以去[官网](http://daringfireball.net/projects/markdown/syntax)学习。当然除了语法我们还需要一款编辑器啦，在此重点推荐一款Mac上最好的Markdown的编辑器[Mou](http://mouapp.com/)。最近该软件的作者打算[拍卖](https://www.v2ex.com/t/113734)该软件的所有权，希望能让更有能力的技术团队能够继续完善该软件。本blog的所有的文章全都是使用该编辑器写的。

![mou](http://lc-4REXSuuT.cn-e1.lcfile.com/6f5f0f0fb9404eaf8058c68e405740bd.png)


## 2.加入评论功能
既然是blog怎么可以没有评论功能呢。Jekyll虽然生成的是静态页面，但是我们不通过写代码和数据库支持也能为期加入评论功能。[Disqus](http://disqus.com/)就是一款社会化的评论系统，我们只要将Disqus生成的一段代码加入到Jekyll模版文件内即能实现网站的评论功能。

1.首先注册Disqus账户，然后点击“Add Disqus to Your Site”按钮。在接下来的页面填写你的blog的基本信息后便完成了站点设置。然后选择"Universal Code"后我们便获得了需要内嵌评论功能的代码了。

![addnewsite](http://lc-4REXSuuT.cn-e1.lcfile.com/9caaa75bc20c4f1e90baedea49384af2.png)

2.将前面获得的代码复制到```_layouts```文件夹下```post.html```文件内的```</article>```和```</div>```标签之间即可。然后我们每发布一篇文章Disqus都会为我们生成相对应的评论功能。（此处使用的是Jekyll默认模版文件）

![addcode](http://lc-4REXSuuT.cn-e1.lcfile.com/e74915422b5641c78f2f074fc416063b.png)

## 3.加入Google Analytics
最后我们再来为我们的网站加上Google Analytics用来统计网站访问情况。登录Google Analytics后创建一个新的站点后，会生成一个唯一的站点内嵌代码，我们将这段代码拷贝下来后复制到```_layouts```文件夹下```default.html```文件内的```</body>```标签之上即可。

![googleanalytics](http://lc-4REXSuuT.cn-e1.lcfile.com/69e9de3ce7b94740ac41217e5e7fd15a.png)
