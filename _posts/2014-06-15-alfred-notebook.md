---
title: "丢掉鼠标－Mac神软Alfred使用手册1"
date: 2014-06-15 19:59:42
categories: alfred
tags: Alfred Mac
key: A-2014-06-15-19-59-42
author: wellsnake
---

__注1：本文写于WWDC 14之前，当苹果在WWDC14上发布了OS X最新版Yosemite的时候，发现其中的Spotlight已经进化了，看上去完全就是和Alfred一个模子里出来的，甚至界面比Alfred更漂亮。不过个人认为这并不影响Alfred在Mac上作为神软的地位，除了Spotlight上的那些功能外，Alfred的神级功能Workflows也是Spotlight无法超越的。另外原来只是打算写个简单的介绍的，不过发现越写越长，索性就叫使用手册吧。__

__注2：关于Alfred的名字由来的猜测，个人觉得作者应该是蝙蝠侠的粉丝。因为蝙蝠侠里那位衷心耿耿的管家就叫Alfred，这也正好说明了Alfred就好像是我们Mac系统的管家，样样精通！__

再开一坑，Mac软件推荐，这次先为大家介绍Mac上的神软[Alfred](http://www.Alfredapp.com)。记得以前在Windows平台有一个叫everything的软件，主要特色就是输入关键字后能够快速得定位出你想要的文件。今天我们要介绍的Alfred也有和它有一样的功能，当然如果只是简单的搜搜文件那也就称不上“神软”了。它不但是搜索工具，还是快速启动工具，甚至能够操作许多系统功能，扩充性极强，如果有兴趣应该还可以写一个煮咖啡的插件出来（嗯，怎么听着好耳熟）。Alfred是一个用键盘通过热键、关键字、自定义插件来加快操作效率的工具。简单点说就是使用了Alfred后你就可以丢掉鼠标了！本次介绍会分两篇来介绍，上篇介绍Alfred免费版和Powerpack版的部分功能（文中所有带 ![pp_icon](http://lc-4REXSuuT.cn-e1.lcfile.com/537bd56d0de9adc78a91.png) 图标的都表示为需要购买Powerpack才能使用的功能），下篇着重介绍Alfred Powerpack的Workflows功能，其实这才是Alfred可以称为神软的功能。当然其实免费版本已经大大为我们提高了效率，不是重度用户使用免费版本也已经够用了。

下图就是Alfred的主界面我们所有的操作都在这一个界面上进行。通过热键打开主界面（本人设置的是option+command），输入一个“a”后Alfred就会为我在候选界面上显示操作系统中所有与“a”打头相关的操作。包括Alfred的设置、搜索亚马逊、a打头的所有app。如果我们继续输入后续的内容，下拉选框内会动态显示候选操作。如果第一行正好是你想要的操作那么直接回车即可，同样我们也可以通过提示的热键来选择后面的操作。

![Alfred_main](http://lc-4REXSuuT.cn-e1.lcfile.com/e99e4aae00c34dc9a0333e86c18071b8.png)

__接下来通过Alfred的设置来深入了解这个“神软”到底有哪些神奇的功能吧。__


## 1.General
![preferences_general](http://lc-4REXSuuT.cn-e1.lcfile.com/3a41147467f44e688c6db5e550994ebc.png)

General的选项很简单

1.`Startup`设置系统启动时是否自动开启。

2.`Alfred Hotkey`设置启动Alfred的热键。

3.`Where are you`这个设置比较特别，因为Alfred内置了常用网站搜索功能，在这里设置了你所在的国家后，Alfred在搜索时会打开搜索网站对应国家的网站。


## 2.Features 

__这里是免费版的重点，Alfred里所有的搜索功能都在这里设置。接下来我们一一介绍：__

### 2.1. Default Results

![default_results](http://lc-4REXSuuT.cn-e1.lcfile.com/cfd00596358040b98bd7956c44a298ca.png)

`Essentials`选项可以设置搜索“应用程序”、“联系人”、“设置”、“Safari书签”、其它的还能查询“文件夹”、“文本文件”、“图片”等其它文件，或者直接选中`Search all file types`选项，不过这里Alfred建议我们可以通过`open`关键字或者`space空格`来查询文件或者文件夹，因为如果全部选中的话不但影响查询速度还容易混淆查询结果。

`Search Scope`设置Alfred查询时会遍历的文件夹，我们在这里可以自己添加和删除文件夹。`Fallcacks`  ![pp_icon](http://lc-4REXSuuT.cn-e1.lcfile.com/537bd56d0de9adc78a91.png) 是设置如果没有查到结果使用google还是其它网站来搜索结果。

__输入关键字查询应用程序__

![search_app](http://lc-4REXSuuT.cn-e1.lcfile.com/34d3b6c1d9b442f7816dcac476b70458.png)

__输入关键字查询联系人__

![search_contacts]http://lc-4REXSuuT.cn-e1.lcfile.com/f30e212c75394967860f2e73d35a2ed7.png

__输入open 关键字查询文件或文件夹__

![search_file](http://lc-4REXSuuT.cn-e1.lcfile.com/6daa8a3a9e814b61b253c5b25c439bfb.png)

__没有找到结果直接通过搜索引擎来查询结果__

![search_file](http://lc-4REXSuuT.cn-e1.lcfile.com/18a80935b7a043fb93334908d49a4879.png)


### 2.2. File Search

__Search选项：__  

![file_search](http://lc-4REXSuuT.cn-e1.lcfile.com/8bf422798d114d4995e399c9de42633a.png)

启用了`Quick Search`选项后我们可以使用`‘单引号`或者`space空格`快速启用打开文件或者文件夹功能类似于使用`open`关键字。

`open`关键字用来打开文件或者文件夹。`find`关键字用来查询文件或者文件夹的位置。`in`关键字用来查找文本文件内含有查询文字的文件（这个功能很强大啊） `tags`关键字用来查询含有查询tags的文件或者文件夹，另外我们还可以选择查询结果中不出现“邮件”、“书签”、“音乐”等其它文件内容。以上查询关键字都能自定义而且也能修改显示结果个数。

__查询文本文件内含有查询条件的文件__

![searc_file_use_in](http://lc-4REXSuuT.cn-e1.lcfile.com/50b27547cfa3441a8f26666acdcc8763.png)

__查询含有tags的文件或者文件夹__

![search_file_use_tags](http://lc-4REXSuuT.cn-e1.lcfile.com/e76371e11b1141119718fecb8d94763e.png)

__Navigation选项：__  ![pp_icon](http://lc-4REXSuuT.cn-e1.lcfile.com/537bd56d0de9adc78a91.png)

![file_navigation](http://lc-4REXSuuT.cn-e1.lcfile.com/32991b5d74264fb1a6fa73ef50c12ffc.png)

这里我们可以设置文件导航工具。我们可以使用`/`来直接定位到根目录或者使用`~`来直接定位到当前用户的home目录。在文件定位工具中我们可以设置是否使用左右建来作为前进或者后退功能。

另外我们还可以通过快速导航功能来调用系统的“预览”工具，并设置相应的快捷键和关键字。

__文件导航工具__

![file_search_navigation](http://lc-4REXSuuT.cn-e1.lcfile.com/013059807d354d1c9650a0c74ebc224c.png)

__Buffer选项：__ ![pp_icon](http://lc-4REXSuuT.cn-e1.lcfile.com/537bd56d0de9adc78a91.png)

![file_buffer](http://lc-4REXSuuT.cn-e1.lcfile.com/55fc177a63e74abfb3fd845dd7d9fafa.png)

这也是Alfred的神奇功能之一，我们可以将查找到的文件或者文件夹加入到缓存中，然后就可以对搜索到的结果做批量处理了。这里的设置也很简单主要就是是否启用缓存功能和缓存功能的几个快捷键，并且可以设置使用完后是否清空缓存等设置。

__通过option键 + ⬆️来将选中的文件夹或者文件加入到缓存，我们可以看到如果存在缓存的话Alfred搜索界面上会出现选中文件的小图标__

![file_search_add_buffer](http://lc-4REXSuuT.cn-e1.lcfile.com/24405b02163a418ca3e47f02f2796d59.png)

__通过option键 + ➡️来批量处理缓存中的文件夹和文件。我们可以打开、发邮件、拷贝、移动、删除（嗯对了你是不是感觉到这个功能就是代替鼠标选中文件然后右键的功能）__

![file_search_buffer_action](http://lc-4REXSuuT.cn-e1.lcfile.com/02d7eeebb399442caed239861afc6cdb.png)

__Action选项：__  ![pp_icon](http://lc-4REXSuuT.cn-e1.lcfile.com/537bd56d0de9adc78a91.png)

![file_actions](http://lc-4REXSuuT.cn-e1.lcfile.com/e9945248a9494443b0ec1a30516eb5c6.png)

这个选项设置的功能基本和上面差不多，主要功能是在查询到文件夹或者文件后选择快捷键来显示操作界面，另外我们还可以在Finder中选中文件夹或者文件后使用快捷键来快速打开相同的操作界面（嗯对的又是把鼠标给抛弃了）。如果只是文件夹被选中的话我们可以有更多的操作可以做，比如：在finder中打开文件夹、查询相似的文件、在控制台内打开文件夹、将目录拷贝粘贴板等。

__查询到文件夹后通过fn键来打开文件夹操作界面__

![file_search_action_search](http://lc-4REXSuuT.cn-e1.lcfile.com/12121763f15d4b9c9caeae4ab6c9a846.png)

__Advanced选项：__

![file_advanced](http://lc-4REXSuuT.cn-e1.lcfile.com/4f5f83463fe441e0bc23a5f601f605a2.png)

`Copy Path`选中该选项后如果使用了将目录拷贝至粘贴板的功能后会在目录前后加上单引号。

`Quick Look`选中该选项后选中查询结果然后使用`shift`键可以使用系统的快速预览功能。

`AppleScript`选中该选项后可以使用`com+o`来打开AppleScript编辑器，而Alfred默认的操作是直接执行脚本。

`Performance`在搜索外部存储文件时使用文件类型图标？（这个没有试过不知道是不是这个功能）。

`Sorting`这个设置应该是每次打开查询结果的文件后会更新文件的"kMDItemFSContentChangeDate"的值（具体作用不明，待google之）。

`Home Folder`设置表示home文件夹字符，默认为`~`

### 2.3. Web Search
![web_search](http://lc-4REXSuuT.cn-e1.lcfile.com/f84bc1cb31304cbf9334c48a0e5bebbd.png)

这里当然是网站搜索的一些设置，我们可以使用Alfred默认的一些搜索功能，或者自己来设置一些自定义设置。图中可以看到已经设置了“亚马逊中国”、“亚马逊日本”、“Google”、“百度”、“bilibili”、“youku”等其它自定义查询。点击`Add Custom Search`后我们就可以自定义查询了。

![web_search_add_custom](http://lc-4REXSuuT.cn-e1.lcfile.com/fa7041f70b9a4a5ea002fd626c06c40a.png)

在设置自定义查询界面中主要设置有：

`Search URL`网站查询的URL每个网站的查询URL可以先通过网站查询功能然后查看浏览器的地址栏就能知道了。当然查询内容使用`{query}`变量来代替。

`Title`这个是设置在查询时Alfred查询主界面显示的提示文字。

`Keyword`查询关键字，尽量使用简短容易辨识的文字。

`Validation`这个是用来测试设置是否有效的。

另外每个查询设置都能设置相应网站的图标，只要将网站图标拖到设置的位置即可。

__使用自定义查询amcn关键字来查询查询亚马逊中国kindle的产品信息__

![web_search_search](http://lc-4REXSuuT.cn-e1.lcfile.com/b95e16bcb1f34aaead8096301d12c883.png)

### 2.4. Calculator

计算器这个就不多说了，主要有两个功能，一个就是直接输入简单的加减运算，一个就是输入`=`来输入复杂的计算，支持许多高级的数学函数。

__标准计算功能__

![calcualtor_standard](http://lc-4REXSuuT.cn-e1.lcfile.com/79ec7237f67c45cfb429ed012cb29fef.png)

__高级计算功能__

![calculator_advanced](http://lc-4REXSuuT.cn-e1.lcfile.com/f96576f0f2704632965bf2b9e53705af.png)


### 2.5. Dictionary

字典功能其实使用的是Mac系统自带的字典，可以设置使用的字典和查询关键字。

__使用di关键字来查询中英字典__

![dictionary](http://lc-4REXSuuT.cn-e1.lcfile.com/bd2454a616a5486bbd7dfab52c4955f4.png)

### 2.6. Contacts ![pp_icon](http://lc-4REXSuuT.cn-e1.lcfile.com/537bd56d0de9adc78a91.png)

__Contacts选项：__

![contacts_contacts](http://lc-4REXSuuT.cn-e1.lcfile.com/0d4840a66a6b4d749568b57e61907f92.png)

这里我们可以设置查询到联系人后使用哪些操作，图中已经增加了点击名字拷贝到粘贴板和点击邮件地址直接发送邮件（系统默认操作），另外Alfred还支持 URL Scheme来打开任意App。

__查询联系人__

![contacts_search](http://lc-4REXSuuT.cn-e1.lcfile.com/30d45f9aeba948398b345e139f9cd864.png)

__联系人详细界面可以选择邮箱地址直接发送邮件__

![contacts_show](http://lc-4REXSuuT.cn-e1.lcfile.com/7ec55b82ccbc44aabf8773d7b2f3b98a.png)

__Email选项：__

![contacts_email](http://lc-4REXSuuT.cn-e1.lcfile.com/3d0455e4462a4be08637a069d1800567.png)

这里是发送邮件的选项。可以设置发送邮件的关键字，也可以设置打开gmail网页来代替系统的邮件app来发送邮件。另外还可以设置如果有单个附件和多个附件的情况下邮件主题栏显示的文字。（此功能主要是和前面文件搜索后发送邮件的功能有关）

__直接发送邮件给搜索到的联系人__

![contacts_send_email](http://lc-4REXSuuT.cn-e1.lcfile.com/1d0dd7ed63b04dff82bbbeb0ddce645c.png)

__Advanced选项：__

![contacts_advanced](http://lc-4REXSuuT.cn-e1.lcfile.com/d7f88e8a09cd4659aa8bc4b8bd323b20.png)

这里可以设置联系人搜索结果的展示，比如：姓和名显示顺序对调、显示职位、显示工作、如果有地图信息还能打开地图。


### 2.7. Clipboard  ![pp_icon](http://lc-4REXSuuT.cn-e1.lcfile.com/537bd56d0de9adc78a91.png)

__History选项：__

![clipboard_history](http://lc-4REXSuuT.cn-e1.lcfile.com/0ae5d68234c84e548d278435ac25201c.png)

这里是查看粘贴板历史记录的选项。

`Clipboard Histroy`用于设置粘贴板历史保存的时间。

`Viewer Hotkey`用于设置打开粘贴板查看器的热键。

`Viewer Keyword`用于设置打开粘贴板查看器的关键字。

`Snippet Keyword`用于设置片段查询的关键字。

`Clear Keyword`用于设置清空粘贴板历史的关键字。

`Ignore Apps`用于设置忽略记录至粘贴板历史的应用程序。

__通过热键打开粘贴板查看器并且可以根据关键字查询所有的记录__

![clipboard_viewer](http://lc-4REXSuuT.cn-e1.lcfile.com/9736ce772b4740a38593923453d5b9d8.png)

__Snippets选项：__

![clipboard_snippets](http://lc-4REXSuuT.cn-e1.lcfile.com/ca1db3f0db3048ef8e047c010b7b12a0.png)

此功能主要是用于设置文本片段便于快速输入用。例如可以输入地址、常用问候语、常用代码片段等。

`Name`文本片段名称

`Keyword`文本片段关键字

`Snippet`文本片段内容

使用时可以通过打开粘贴板浏览器根据名称和关键字查询，或者直接使用前面设置的片段查询关键字来查询

__使用snip关键字查询文本片段__

![clipboard_snip_search](http://lc-4REXSuuT.cn-e1.lcfile.com/650f34eb2cdb4019b576b04c0d0c4613.png)

__查询到结果后直接回车便能将片段内容输入到当前激活的应用程序内__

![clipboard_snip_used](http://lc-4REXSuuT.cn-e1.lcfile.com/6806dc9b5bf644798248fa80d4aed6ae.png)


__Merging选项：__

这是一个神奇的功能：当我们复制了一段文本后，再选中另外一段文本后，通过使用`command＋C＋C`热键可以将当前选中的文本追加到第一次复制的文本后面。并且可以设置是使用空格、回车来分割不同的片段。

__最后一段文字是使用了merging功能快速粘贴出来的__

![clipboard_merging](http://lc-4REXSuuT.cn-e1.lcfile.com/995e9657a01b4d1c9c9d2853df2b7f4a.png)

__Advanced选项：__

这里主要设置自动粘贴当前选中的记录和设置复制文本内容的最大字节。


### 2.8. iTunes  ![pp_icon](http://lc-4REXSuuT.cn-e1.lcfile.com/537bd56d0de9adc78a91.png)

__General选项：__

![itunes_general](http://lc-4REXSuuT.cn-e1.lcfile.com/934d0a8c59c2418ea9e8bb01b4c58fd0.png)

这个功能就类似一个iTunes的迷你播放器。

`Mini Player`用来设置打开迷你播放器的热键和关键字。

`Playback`如果使用随机选择专辑命令，Alfred只会选择歌曲数目大于5的专辑。

`Behaviour`查询并选中歌曲后自动关闭迷你播放器界面。

`Searching`查询歌曲后Alfred会自动在iTunes内添加播放列表

__Afred的Mini Player,可以输入各种关键字来控制播放__
![itunes_miniplayer](http://lc-4REXSuuT.cn-e1.lcfile.com/f54d45d9d53944adb2e779ec0624d2b0.png)

__Keywords选项：__

![itunes_keywords](http://lc-4REXSuuT.cn-e1.lcfile.com/795a285fcd344f10affaf3c63d844b79.png)

这里主要用于设置iTunes播放命令的关键字。主要有：播放、暂停、下一曲、上一曲、随机选择专辑、最大音量、一半音量、静音。另外选中了`Show these keywords in Alfred Default Results`后不但可以在迷你播放器内使用这些命令还能在搜索界面内使用以上命令。

__直接在Alfred搜索界面输入下一曲的命令__

![itunes_next](http://lc-4REXSuuT.cn-e1.lcfile.com/9e44af32342c4ffc8922e46229c1225b.png)

__在迷你播放器内输入随机播放的命令__

![itunes_random](http://lc-4REXSuuT.cn-e1.lcfile.com/bc95a87b3ea34dcb8c21800974d71905.png)

__Advanced选项：__
![itunes_advanced](http://lc-4REXSuuT.cn-e1.lcfile.com/cab4925c332841fb9d0d306ffa1a1b26.png)

这里主要设置iTunes的资料库目录，如果Alfred没有找到我们可以手动设置。另外Alfred还能查询不在iTunes资料库内的歌曲。我们还可以设置Alfred在iTunes内的播放列表的名称。

### 2.9. 1Password ![pp_icon](http://lc-4REXSuuT.cn-e1.lcfile.com/537bd56d0de9adc78a91.png)

![1password_config](http://lc-4REXSuuT.cn-e1.lcfile.com/1315d4a8b8bb403594fc3cb732ca1e00.png)
如果你购买了1Password这个Mac上的密码管理软件（另外一个神软的）的话，我们就可以直接在Alfred内直接搜索密码库了。不过需要注意的是如果Alfred显示`Unable to find 1Password Data`的话我们需要打开1Password的`启用与第三方应用整合`这个选项。

![1password](http://lc-4REXSuuT.cn-e1.lcfile.com/ade70f618ad34f669723e4096f91a1a8.png)

__使用关键字来查询1Password密码库__

![1password_search](http://lc-4REXSuuT.cn-e1.lcfile.com/5cf5aa4d07de45cb87e61227ff8410ad.png)


### 2.10. System

![system](http://lc-4REXSuuT.cn-e1.lcfile.com/a4e3d9a6a9f24bd2b79e1aae0b3120e6.png)
这里主要是设置一些系统命令的关键字。

`常规系统命令:`屏幕保护程序、显示回收站、清空回收站、登出、睡眠、锁定、重启、关机

`程序管理命令:`隐藏、关闭、强制关闭、关闭所有应用程序

`盘符管理命令:`推出某个盘符、推出所有盘符、设置盘符黑名单

### 2.11. Terminal/Shell ![pp_icon](http://lc-4REXSuuT.cn-e1.lcfile.com/537bd56d0de9adc78a91.png)

![terminal](http://lc-4REXSuuT.cn-e1.lcfile.com/14358a322daa47b0bfa3f3b1e910c2df.png)

Alfred还能输入控制台命令。这里设置比较简单了，设置输入命令的关键字和使用的默认控制台程序。

__在Alfred搜索界面输入控制台命令__

![terminal_command](http://lc-4REXSuuT.cn-e1.lcfile.com/bf6cbc787c1b46a6bcf36f7598adff1a.png)

__好了，终于把上篇Alfred的基本功能全都说个了遍，基本上没有啥遗漏的功能了。如果能掌握上面所有的功能的话已经能够减少大部分的鼠标操作和重复性操作，大大提高操作系统使用效率。下篇将介绍Alfred的另外一项重要功能Workflows，敬请期待......__


