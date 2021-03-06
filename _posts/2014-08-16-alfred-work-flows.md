---
title: "杀手级功能WorkFlows介绍(1)-Alfred使用手册2"
date: 2014-08-16 23:45:42
categories: alfred
tags: Alfred Mac WorkFlow
key: A-2014-08-16-23-45-42
author: wellsnake
---

## 前言
等了那么久，Alfred用户手册第二篇也终于出来了！上一篇中详细介绍了Alfred的基本查询功能和一些收费功能。第一次写这么长的教程收到了不少读者好评也给了很多意见。有细心的读者还给我提交了Alfred的Bug，为了给读者一个答复我用非常蹩脚的英语给Alfred官网提交了Bug很快便得到了回复，具体Bug信息可以参见[上一篇](http://wellsnake.com/jekyll/update/2014/06/15/001/ "Alfred用户手册1")的评论。

本篇将着重介绍Alfred杀手级功能WorkFlows。个人认为这个功能才是Alfred的核心功能，有了这个其它那些免费功能只能打打酱油了。说的那么厉害那么WorkFlows到底能做什么的呢？在Alfred官网是这么介绍的：

**From quick file filters to advanced scripts, you can control your Mac, other applications, web services and more.**

我们可以通过高级脚本语言来快速过滤文件、控制Mac、应用程序、web services甚至更多。有的人就想了这些貌似免费版也能做啊？注意是 *高级脚本语言* 免费版只是事先定制好的一些功能，而WorkFlows则是可以通过用户自己写脚本语言来定制搜索和其它一些高级功能。查了下WorkFlows支持`bash`、`zsh`、`php`、`ruby`、`python`、`perl`、`osascript`这些脚本语言。看到这些估计很多程序猿们已经开始蠢蠢欲动了吧。

支持脚本语言还只是WorkFlows的一部特性，难道不懂代码的小白们就用不了了吗？非也非也。我们再来看看WorkFlows的实现机制吧，在官网上还有这么一段介绍：

**Put simply, workflows allow you to connect triggers and keywords to actions and outputs. Once they're connected together, you're up and running!**

从这段话中我们可以看到实现WorkFlows的四个基本对象：`trigger`、`keyword`、`action`、`output`。Alfred通过将这四个基本对象合理connect便能实现各种高级功能。就好像乐高玩具，我们可以通过各种零件组合在一起组装成各种有趣的形状。可以夸张的说WorkFlows没有什么做不到只有你想不到的。下面是我画的一张思维导图，下面我便通过这张图由浅入深一一介绍WorkFlows的方方面面。

![createworkflow](http://lc-4REXSuuT.cn-e1.lcfile.com/ce6bf721acc14c54a37bafbb6f6372a7.png)

## 1. Examples
Alfred安装完后内置了7个例子。我们先不逐一介绍WorkFlows的四个基本对象，那样太理论化了。对于小白用户我们可以通过研究学习这几个例子来了解WorkFlows的使用方法，并从例子里逐步了解这四个基本对象。

### 1.1. Should I watch this movie
我们通过点击“＋”号，选择“Examples”－“Should I watch this movie”就添加成功了，其它的例子添加方法一样。我们双击名字可以打开WorkFlows的一些属性设置，这个界面每个WorkFlows都是一样的。

![workflows\_details](http://lc-4REXSuuT.cn-e1.lcfile.com/5c8dbe5388354b3684524bf405cf3050.png)

其中可以看到有以下这些属性：
`Workflow Name`名字
`Description`功能描述
`Category`类型，有未分类的、工具类、互联网类、生产率类的
`icon`将图片拖进框内，为WorkFlows设置图标
`Bundle id`为WorkFlows取一个唯一的可辨识的ID
`Created by`作者
`Website`主页
`Readme`如果还有其它的内容需要填写我们可以都填写在这里

![workflows\_should\_i\_watch\_this\_movie](http://lc-4REXSuuT.cn-e1.lcfile.com/e370aa266efb45b19caf7e76dbce33b5.png)

从功能描述中我们可以知道，这个WorkFlow的功能是通过关键字“movie”加上电影名字然后系统会打开浏览器并分别从Youtube查询电影预告、从IMDB查询电影详细信息、从Rotten Tomatoes查询电影评分。除了基本设计外，我们下面来详细介绍这个WorkFlow的“组装”界面：

![workflows\_master](http://lc-4REXSuuT.cn-e1.lcfile.com/dc4ed4f161a44cd08ad9179a6943a1f4.png)

从上图中我们可以看到这个WorkFlow由2个基本对象组成：1个`Input`和3个`Action`。其中使用了`Input`的`Keyword`控件（姑且这么叫吧），和`Action`的`Default Web Search`和`Open URL`控件，并且`Input`和`Action`之间用3条线连接了起来。联系前面说到的功能描述是不是觉得这个“组装台”界面很形象啊！我们再点开每个“零件”看看里面的设置又是怎样的。

![workflows\_input\_keyword](http://lc-4REXSuuT.cn-e1.lcfile.com/dd1cc40dca08484b944f8e1d0c4b0422.png)

点击`Keyword`控件，我们可以看到如上界面，主要可设置**关键字**、**是否需要参数**、**查询标题**、**查询说明**。

![workflows\_action\_web\_search](http://lc-4REXSuuT.cn-e1.lcfile.com/e3b226cd31094618bdca466c874db57d.png)

点击其中一个`Default Web Search `控件，我们可以看到如上界面，主要可以设置搜索的网站和打开的浏览器。这里的搜索网站都是Alfred预设的，可当我们从中找不到我要搜索的网站怎么版那么就要用到下面一个控件了。

![workflows\_action\_open\_url](http://lc-4REXSuuT.cn-e1.lcfile.com/8e4228b217c04a8da88ee0d0ed55139e.png)

`Open URL `控件就可以自定义查询网站，打开该控件我们可以设置URL。URL由网站的搜索URL＋{query}关键字组成。如果不知道搜索URL是多少，我们可以先使用一次网站的搜索功能然后就能在浏览器的地址栏上找到该网站的搜索地址了。还能设置将查询内容编码成UTF8格式、将查询内的空格变成＋号。

讲到这里聪明的读者一定会想以上3个网站在天朝都被墙了，这个WorkFlow没法用啊，不如把豆瓣等国内的电影网站搜索功能给加上去呢。那么我们就动动手一起把豆瓣电影搜索给加上去吧。很简单我们只要再加入一个`Action`就可以了，不过在`Default Web Search`控件的列表里找不到豆瓣，那么我们只能用`Open URL`了。点击“＋”号依次选择“Action”－“Open URL”，然后“组装台”上就多了一个控件了，我们将`Keyword`控件和新加入的`Open URL`控件先连接起来，然后再双击该控件，然后在URL中输入“http://movie.douban.com/subject\_search?search\_text={query}”其它设置默认即可。至于这个搜索连接是怎么获得的呢？其实很简单我们只要使用网站的搜索功能后就能在浏览器的地址栏上就能看到搜索连接了。

设置完后我们来试用一下，在Alfred搜索界面中输入“movie star wars”后浏览器会同时打开4个网站，而第四个网站就是我们新建的豆瓣电影的搜索结果了。是不是突然觉得建一个WorkFlow其实很简单呢？

![workflows\_douban\_search](http://lc-4rexsuut.cn-e1.lcfile.com/5b47e0420940499f9f7f93fa8ba85c92.png)

### 1.2. Google Suggest

![workflows\_google\_suggest](http://lc-4REXSuuT.cn-e1.lcfile.com/a0a43d8153e6427c84d6045e6cf818e3.png)

这个WorkFlow的功能是让我们在使用Google查询功能时能够使用只有在网页端查询才有的Google Suggest功能。就是在每次输入查询内容时系统会列出一些候选的查询关键字供用户选择。当然由于我们伟大的qiang存在无法正常使用该功能，所以大家就看看我的截图吧。
当然这个不是我要说的重点，其实这个WorkFlow是整个使用手册里最难入门的一个了，因为它里面用到了`Script Filter`控件。这个控件是需要我们编写代码才能实现相关功能的，一旦掌握了这个技巧，那么Alfred基本就无所不能了。不过如果是代码小白可以直接跳过这一章了，当然你想折腾下那就接下去看吧。前面我也说过了Alfred支持许多脚本语言，由于本人对Python比较熟悉所以整篇文章就以Python为主了。
首先我们先来分析下这个例子（这个例子里使用的脚本语言是PHP）

![workflows\_google\_suggest\_detail](http://lc-4rexsuut.cn-e1.lcfile.com/cee8e8ff7af443aca116f1b089ee5a4c.png)

从上图中我们可以知道这个WorkFlow使用了一个`Script Filter`控件，并将查询的结果传递给`Default Web Search`控件。然后我们双击`Script Filter`控件看看里面是怎么设置的。

![workflows\_google\_suggest\_script](http://lc-4REXSuuT.cn-e1.lcfile.com/d6b4a1346c4d4a6f92c1692976cc4b3b.png)

`Keyword`关键字
`Placeholder Title`WorkFlow使用时的标题
`Placeholder Subtext`WorkFlow使用时的提示文字
`Please Wait Subtext`WorkFlow在查询时提示的文字
`Language`使用的脚本语言
`Escaping`在脚本内需要过滤的一些特殊字符防止脚本执行时受干扰（这个有疑问？）
`Script`脚本
别的设置其实都比较简单，关键就在Script这块了，我们可以看到代码第一行有一句
`require_once('workflows.php'); `
这里是在执行脚本之前需要先倒入**workflows.php**这个文件，这个文件是Alfred提供给我们封装了所有我们要编写WorkFlow方法的库文件。这个文件放在哪里呢？我们点击**Open workflow folder**就能看到了。

![workflows\_google\_suggest\_folder](http://lc-4REXSuuT.cn-e1.lcfile.com/1c7278ffc6dd41aa8ed4ed227ea7de1e.png)

上图中这个是PHP版本的库文件，当然其他的脚本语言也有对应的库文件，我们可以在[官方论坛](http://www.alfredforum.com/topic/2030-workflow-libraries-and-helpers/)里找到。
然后我们来简单介绍下这段代码主要做了什么吧
- 程序访问了Google Suggest的API并将在Alfred输入框输入的查询内容传入API的传入参数内
- 然后开始逐一解析API返回回来的结果，这里返回结果格式是XML的
- 最后调用WorkFlow库内的方法将内容组织成Alfred的返回结果（result函数），主要内容有标题、标题下面的提示文字、图标、传出参数（供其他控件调用）

上面说了那么多大家肯定还是一头雾水，不如我们直动手来的直接。我们就做一个豆瓣图书查询的WorkFlow吧，先来看看我研究了几天的成果吧。

![workflows\_douban\_book](http://lc-4REXSuuT.cn-e1.lcfile.com/7f94222f8c7d4870bba8d689fb688a57.png)

这个WorkFlow的功能是输入**douban**关键字后我们输入任意需要查询的图书名字，Alfred为我们列出与名字相匹配的图书结果。结果中我们可以了解到图书的书明、作者、出版社、价格、评分。并且选中某本书后系统会打开浏览器直接跳转到该书的详细页面。好，下面开始动手！
首先添加一个**Blank WorkFlow**,设置如下图

![workflows\_douban\_book\_details](http://lc-4REXSuuT.cn-e1.lcfile.com/88fcaa0ffe2c4e09ae8d03cd9eeca53e.png)

`WorkFlow Name`WorkFlow的名字
`Description`功能描述
`Category`类别
`Bundle id`WorkFlow的一个唯一ID号，最好以你自己的域名＋WorkFlow名字
`Created By`作者
`Website`作者的网站
设置好后，Alfred就会为WorkFlow创建一个文件夹并且生成一个名叫**info.plist**的文件，在使用WorkFlow库的时候会调用这个文件，所以一定要先做这一步。然后从GitHub上[下载](https://github.com/deanishe/alfred-workflow)Python版的WorkFlow库，并解压到**info.plist**同一个目录下。然后再新件一个**douban.py**脚本文件。最后文件结构如下图

![workflows\_douban\_folder](http://lc-4REXSuuT.cn-e1.lcfile.com/265db5e982904545ad0cff9d8368166d.png)

然后就开始写代码了，打开**douban.py**输入如下代码，具体代码可以访问我的[Gist](https://gist.github.com/wellsnake/b8ddd8f11d4b712af3fd)。

![workflows\_douban\_book\_script](http://lc-4REXSuuT.cn-e1.lcfile.com/3173987087854e439884ab251899753c.png)

上面代码中豆瓣图书查询API在豆瓣开发者页面内有相关的文档，每个接口的调用方法和返回结果都有一一说明的，这里就不展开了，大家可以去[这里](http://developers.douban.com/wiki/?title=guide)了解详细内容。另外上面写好的代码是可以直接在控制台或者在编辑器内调试运行的，在控制台内我们只要输入`python douban.py 查询内容 `就可以看到执行结果了，本人使用的是Pycharm可以设断点调试比直接写在Alfred的Script内要方便多了。好了接下来就要告诉Alfred怎么调用我们写好的代码了。首先在我们的WorkFlow界面内增加一个`Script Filter`控件，具体设置如下

![workflows\_douban\_script\_filter](http://lc-4REXSuuT.cn-e1.lcfile.com/a1c705d6e14449c29f7ffe76bb9ed61c.png)

其中要注意的就是因为我们的代码是直接写在脚本文件内的与之前例子写在Script内不同，所以我们这里要在Script内写`python douban.py "{query}" `并且**Language**选择**/bin/bash**保存后我们就可以直接使用了。在Alfred搜索界面输入`douban 图书名`就能在列表中看到搜索结果了。如果只是看看简单的图书介绍那么到这里就结束了，不过如果我们想选中某本书并且打开浏览器看看图书的详细信息的话就要用到`Action`控件了。我们还是在WorkFlow界面上新增一个`Open URL`的`Action`控件。然后在控件的配置界面里将URL设置成`http://book.douban.com/subject/{query} `，在这里的**{query}**就是前面的`Script Filter`控件代码中的`arg=post['id'] `这个值。
最后一步不但简单也很形象，我们要将刚才创建的两个控件链接起来，我们要将`Script Filter`控件返回的参数传递给`Open Url`控件,`Open URL`控件根据接受到的参数打开浏览器并打开相对应的链接。刚建完的两个控件是相互独立的，如下图

![workflows\_douban\_book\_unlink](http://lc-4REXSuuT.cn-e1.lcfile.com/da338ee7f4b3430d842e64e8dfec11a5.png)

我们要做的就是将鼠标移动到`Script Filter`控件上，然后就能看到控件右边会有一块突出的部分，然后鼠标按住突出部分并移动到`Open URL`控件边缘后放开鼠标就将两个控件连接起来了。最终效果如下图

![workflows\_douban\_book\_link](http://lc-4REXSuuT.cn-e1.lcfile.com/4710043fec6547588e8712c403739efe.png)

**通过以上这些我们基本已经从无到有创建了一个可用的WorkFlow了，其实这个WorkFlow我们还可以继续扩展，比如加入电影搜索，音乐搜索等其他更丰富的功能。而且我想通过以上的介绍大家应该也已经对Alfred的WorkFlow有更深入的了解了吧！最好的学习办法就是动手实践，我建议大家可以拿自己熟悉得脚本语言和熟悉的Web API来做一个WorkFlow。当然除了以上介绍的内容外WorkFlow还有好多东西要讲呢，所以光一篇是讲不完的，我会在下一篇继续介绍WorkFlow下其它控件的用法，并且会继续完善这个豆瓣查询的WorkFlow的。那么下次见**
