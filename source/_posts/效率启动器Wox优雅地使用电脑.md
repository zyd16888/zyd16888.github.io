---
title: Windows上的效率启动器Wox，教你如何优雅地使用电脑
tags:
  - windows
categories: 系统
copyright: true
abbrlink: 98bc273a
date: 2018-04-19 23:23:32
password:
---
&emsp;&emsp;在日常的电脑使用操作中，我们常常需要花很多的时间去做同一件事情，比如启动软件的操作：点击开始菜单->寻找软件图标->点击启动。为了方便我们快速的启动软件，我们通常还会把最常用的软件图标放到任务栏当中，你或许以为这就是启动软件的极限操作了。但是，我今天要告诉你的是一款效率神器Wox，教你如何优雅地使用windows电脑，而它的作用不仅仅在于快速启动软件。
{% meting "921690953" "netease" "playlist" "autoplay" "mutex:false" "listmaxheight:340px" "preload:none" "theme:#ad7a86"%}
&emsp;&emsp;Wox是一款windows下的免费开源软件，学习门槛低，能够通过快捷键快速地调用并完成自己想要的操作，整个过程表现的十分流畅，是一款大家普遍用完之后爱不释手的效率软件。它主要具有以下几个方面的功能：

+ **快速启动** 支持中文模糊搜索，甚至支持绿色软件快速启动。
+ **网页搜索** 支持在Wox搜索框中直接输入网址或者需要搜索的关键词，然后自动跳入到浏览器中进行搜索。
+ **文件夹/文件搜索** 利用everything插件，支持进行本地所有硬盘文件夹以及文件搜索。
+ **插件管理** Wox得益于强大的插件管理，通过Wox搜索框可以完成有道翻译、快速计算器、搜索浏览器书签并打开、移除USB、命令行操作、关机等等。



<font color=#0099ff> Wox - 被誉为 Alfred 的 Windows 版最佳替代品</font>
&emsp;&emsp;你可以将 Wox 看作一个高效的本地快速搜索框，通过快捷键呼出，然后输入关键字来搜索程序进行快速启动，或者搜索本地硬盘的文件，打开百度、Google 进行搜索，甚至是通过一些插件的功能实现单词翻译、关闭屏幕、查询剪贴板历史、查询编程文档、查询天气等更多功能。
![ ](http://data.singlelovely.cn/xsj/2018/4/20/wox1.png)

&emsp;&emsp;Wox 最大的特点是可以支持中文拼音的模糊匹配。譬如说你想搜索“设备管理器”，那么只需输入"sheb"就能匹配得到。

<font color=#0099ff>增加程序的搜索目录：</font>

&emsp;&emsp;一开始使用 Wox 时，你会发现，除了开始菜单里面有的程序能搜索到之外，自己的一些绿色软件或者安装到非默认目录的软件都找不到。这时你可以在 Wox 里输入 settings 回车或托盘图标右键选择 Settings 进入设置界面，然后在 程序 中按 增加 按钮添加你的软件所在的文件夹。
![ ](http://data.singlelovely.cn/xsj/2018/4/20/wox2.png)

<font color=#0099ff>网页搜索功能：</font>
&emsp;&emsp;Wox 的网页搜索功能是可以让用户自己为某个搜索引擎设置一个关键字。举个简单例子，如果用户经常使用百度搜索。那么用户就可以在 Wox 的设置里的 Web Search 选项中，点击 Add 增加这么一个选项（URL为 http://www.baidu.com/s?wd={q}）：

<font color=#0099ff>搭配Everything</font>
wox已经有everything的SDK，但如果你想更强大的搜索，可以在wox的release页面下载everything进行默认的安装。

如果在wox搜索时，下方显示everthing not runing，可以打开everything的窗口。

或者在安装时选择：为everything安装服务而不是以管理员身份运行。

<font color=#0099ff>其他插件：</font>

**witcheroo(多个任务之间切换)**

    wpm install Switcheroo for Wox
使用方法：win 窗口标题

**ProcessKiller（结束进程）**

    wpm install Wox.Plugin.ProcessKiller
使用方法：kill 进程名

**Clipboard History（剪粘板历史记录）**
     
	wpm install Clipboard History
使用方法：wox中输入：cb 就会列出历史记录
eg: cb

**有道翻译**

    wpm install 有道翻译
使用方法：yd 要翻译的英文
(eg:yd test )

**OpenCMD（当前文件夹打开CMD）**
  
    wpm install Wox.Plugin.OpenCMD
使用方法：在当前文件夹，运行wox，输入op

**IP Address**

    wpm install IP Address
使用方法：运行wox，输入ipadr


注意：wox默认替换Win+R，如下图，不需要可以在设置中关闭
![ ](http://data.singlelovely.cn/xsj/2018/4/20/wox3.png)