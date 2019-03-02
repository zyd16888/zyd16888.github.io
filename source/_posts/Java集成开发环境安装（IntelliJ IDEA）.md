---
title: Java集成开发环境安装
copyright: true
abbrlink: 38df1aba
notshow: false
tags:
  - Java
  - 教程
categories: Java
date: 2018-09-04 15:17:00
password:
description: IntelliJ IDEA 的安装与配置
image:
- "http://data.singlelovely.cn/CoverPicture/38df1aba.png"
sticky:
---


{% meting "1300423074" "netease" "song" %}

 &emsp;
 &emsp;
 &emsp;
>[IntelliJ IDEA相比于Eclipse的优势](https://blog.csdn.net/XuNeely/article/details/78943085)


### 安装 

<span id="font-blue">下载地址: </span>https://www.jetbrains.com/idea/download/?fromIDE=#section=windows

Community 版本为开源免费版
Ultimate  为企业版，试用期一个月

<div class="note success"><p>版本请自行选择，建议使用<span id="inline-yellow">Community</span> </p></div>

然后打开安装，选择安装目录后，会出现如下界面，选择适合自己系统的版本，Java必选，后面的按需选择

![idea安装](http://data.singlelovely.cn/xsj/2018/9/4/idea安装.png)

完成安装后，进行配置，第三项为不采用旧设置

![idea设置](http://data.singlelovely.cn/xsj/2018/9/4/idea设置.png)

然后选择jdk安装路径后，进入主界面

jdk选择界面忘了截图了·······

![主界面](http://data.singlelovely.cn/xsj/2018/9/4/idea界面.png)

### 主题颜色美化

#### 使用Color Themes主题模板


![colorThemes主题展示](http://data.singlelovely.cn/xsj/2018/9/4/colorThemes主题展示.png)

![colorThemes主题展示2](http://data.singlelovely.cn/xsj/2018/9/4/colorThemes主题展示2.png)


上面这是少部分截图，有太多的主题，有兴趣的自己去看一下，总有一款适合你。
使用方式如下：
（1） 找到你喜欢的主题模版，点击右下角的下载按钮，进入如下图：

![colorThemes主题下载](http://data.singlelovely.cn/xsj/2018/9/4/colorThemes主题下载.png)

点击上图中的绿色的按钮下载。
（2）下载下来是一个很小的 Jar包，我们直接包jar包导入Android Studio 。在Android Studio 上 点击 File －> Import Settings ，选择中下载的jar 包，来到如下界面：

![enter description here](http://data.singlelovely.cn/xsj/2018/9/4/安装主题.png)

（3）如上图，点击确认，会提示重启 IntelliJ IDEA  ，点击OK 重启 IntelliJ IDEA 就好。
（4）重启之后，主题就已经应用上了，如下图：

![colorThemes主题效果](http://data.singlelovely.cn/xsj/2018/9/4/colorThemes主题效果.png)


Color Themes 上面有很多主题模版，你自己去挑选就好了。

#### Material Theme UI

使用 Material Theme UI 插件主题：
通过上面的方法，就能为 IntelliJ IDEA 应用一个自己喜欢的个性化主题，但是有一个缺点：这些主题只更改了代码编辑区域，左边的包结构区域和菜单栏还是和原来是一样的，看起来和整体风格好像不是很搭，那么有没有可以使整个AS的风格都改变的主题呢？通过Google ,找到了Material Theme UI,原文地址[Making Android Studio pretty](https://meedamian.com/post/deuglifying-android-studio/)，Material Theme UI 是一个 IntelliJ IDEA 插件，它提供了三种主题供选择，效果非常不错，更赞的是，它连除了代码区域之外的风格也改变了，应用了Material Theme UI 主题的效果图如下：
 
![MaterialThemeUI](http://data.singlelovely.cn/xsj/2018/9/4/MaterialThemeUI.png)

为避免重复造轮子，使用方法请直接查看 Material Theme <span id ="font-green">[原文](https://meedamian.com/post/deuglifying-android-studio/)。

### 花式LogCat

前面介绍了几种打造炫酷主题的方式，效果已经非常赞了，但是我们看一下我们的Logcat ,只有白色和红色两种Log,看起来有点Low ,与我们炫酷的主题不搭啊，因此我们还得改造一下控制台的Log输出。更改之前的效果如下：

![LogCat旧](http://data.singlelovely.cn/xsj/2018/9/4/LogCat旧.png)

<p id="div-border-left-purple">打造花式Log的方法：</p>
（1） 在Android Studio 菜单栏 打开** Preferences －> Editer －> Colors & Fonts －> Android Logcat**

（2） 在Scheme选项后面点击Save As... 保存一个拷贝，在拷贝上面更改，总共有六项，如下图所示，选中每一项依次更改。

![花式logcat](http://data.singlelovely.cn/xsj/2018/9/4/花式logcat.png)

最终效果如下图所示

![LogCat新](http://data.singlelovely.cn/xsj/2018/9/4/LogCat新.png)

如上图所示，效果是不是好了很多！！！也与我们的整体主题风格搭配。贴一下我使用的各项颜色值：
{% cq %}
<font color = "#AA66CC">Assert: #AA66CC</font>
<font color = "#33B5E5">Debug: #33B5E5</font>
<font color = "#FF4444">Error: #FF4444</font>
<font color = "#99CC00">Info: #99CC00</font>
<font color = "#FFFFFF">Verbose: #FFFFFF</font>
<font color = "#FFBB33">Warning: #FFBB33</font>
{% endcq %}