---
title: Genymotion 解决虚拟镜像下载速度特别慢的问题
tags:
  - Android
categories: Android
copyright: true
abbrlink: c9feff90
date: 2018-03-06 09:47:08
password:
---

Genymotion下载地址（需注册账号）：https://www.genymotion.com/download/

Genymotion号称android模拟器中运行最快的，但是服务器在国外，Android镜像下载起来那个速度就不想说了。

Add new device后下载速度太慢了，容易失败



解决方法如下：

方法一：

1、设置HTTP代理，在Setting->Network，自己设置HTTP proxy和Port，

 

方法二：

1、找到下载链接，直接用迅雷拖下来

     遇到下载失败或者下载太慢，win+R打开运行框，输入 %appdata%， 再点击上一步（Alt+↑ ），找到local文件夹里的Genymobile,打开 查看里面的genymotion.log文件，

找到类似下面的文字

[Genymotion] [Debug] Downloading file

"http://files2.genymotion.com/dists/4.1.1/ova/genymotion_vbox86p_4.1.1_151117_133208.ova"



将http://file........ova 这个虚拟镜像地址直接用迅雷极速版下载，或者使用迅雷离线下载等功能很快能完成下载



2、把下载的文件复制到C:\Users\用户主目录\AppData\Local\Genymobile\Genymotion\ova 中覆盖里面以随机数命名的对应镜像。实际上就是刚才看到genymotion软件刚刚点击下载的那个镜像，



3、重新按照刚刚下载操作GUI的下载步骤，你会发现对应的镜像已经可以使用了不需要下载了，验证安装后即会显示在设备列表中。

点击start ，启动模拟器，开始使用





提供两个下载地址：

http://files2.genymotion.com/dists/4.2.2/ova/genymotion_vbox86p_4.2.2_160608_211959.ova

http://files2.genymotion.com/dists/6.0.0/ova/genymotion_vbox86p_6.0_160608_210807.ova