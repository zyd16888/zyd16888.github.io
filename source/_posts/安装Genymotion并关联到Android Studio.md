---
title: 安装Genymotion模拟器并集成在AS中
tags:
  - Android
categories: Android
copyright: true
abbrlink: fec62b1b
date: 2018-03-08 20:47:08
password:
---


&emsp;&emsp; Genymotion模拟器是面向开发者的一款安卓模拟器，运行速度快，功能强大，体积小，占用系统资源少，安装完成后可以集成在Android Studio 或者 Eclipse 中，一键调用进行项目调试。

### 安装Genymotion

#### 注册  下载

&emsp;&emsp; 去genymotion的[官网][1]注册下载，下载之前必须要注册，登录选项在注册按钮里面

![][2]

然后去下载页面下载，genymotion需要依赖VirtualBox，如果没有装过VirtualBox，请下载带VirtualBox版本的（注意
VirtualBox一般不需要升级，以免出现不必要的问题）

![][3]

#### 安装

附：VirtualBox的界面，一般不需要打开，其他软件会自己调用

![][4]

下载后安装，安装路径自己指定一个，然后一路点下一步就行了

#### 创建模拟器

![][5]

首次打开genymotion会提示许可协议，同意就好

![][6]

然后会提示输入授权码，可以去官网买一个，或者点Personal Use（个人用户免费）

![][7]

然后会扫描你电脑上的模拟器，没有的话就会提示添加

![][8]

点击确认后，会有一个登陆账号的步骤
然后就会看到可以创建模拟器的系统选项，选一个想要的系统版本，点击next开始下载

![][9]

![][10]

注： 同一api的模拟器在下载了一次以后就不需要下载了，下次创建会瞬间创建成功。
完成以后点击start就可以启动模拟器了

![][11]

![][12]


### 将genymotion集成在AS中

进入AS中，安装genymotion插件
安装步骤见官网说明：https://www.genymotion.com/plugins/

#### AS中安装genymotion插件

打开File——Settings——Plugins——Browse Repositories界面

![][13]

![][14]

搜索找到genymotion，点击install安装
安装完会在主界面上多一个图标

![][15]

#### 将AS与genymotion关联

点击打开，然后设置genymotion的安装目录，如果没有报错就正常
进入genymotion的设置中，选择ABD，然后选择使用SDK，输入电脑上的SDK存放目录

![][16]

重启AS和genymotion

在AS中打开genymotion插件就能看到已经安装的模拟器了

然后就可以用了···········



ps：使用genymotion后可以将Android SDK中的system imagine文件删掉。

system imagine相当于谷歌系统镜像，genymotion也会下载系统镜像，但system imagine一个api版本5G左右，genymotion一个版本400M左右，可以节省大量空间，且genymotion模拟器的功能更加全面。






  [1]: http://www.genymotion.net
  [2]: https://data.singlelovely.cn/xsj/20182/genymotion1.png
  [3]: https://data.singlelovely.cn/xsj/20182/genymotion%20%282%29.png
  [4]: https://data.singlelovely.cn/xsj/20182/genymotion%20%283%29.png
  [5]: https://data.singlelovely.cn/xsj/20182/genymotion%203.png
  [6]: https://data.singlelovely.cn/xsj/20182/genymotion%206.png
  [7]: https://data.singlelovely.cn/xsj/20182/genymotion%20%2810%29.png
  [8]: https://data.singlelovely.cn/xsj/20182/genymotion%20%287%29.png
  [9]: https://data.singlelovely.cn/xsj/20182/genymotion%20%284%29.png
  [10]: https://data.singlelovely.cn/xsj/20182/genymotion%20%285%29.png
  [11]: https://data.singlelovely.cn/xsj/20182/1519211198852.jpg
  [12]: https://data.singlelovely.cn/xsj/20182/1519211344303.jpg
  [13]: https://data.singlelovely.cn/xsj/20182/1519211955563.jpg
  [14]: https://data.singlelovely.cn/xsj/20182/1519211990273.jpg
  [15]: https://data.singlelovely.cn/xsj/20182/1519212111510.jpg
  [16]: https://data.singlelovely.cn/xsj/20182/1519212300865.jpg