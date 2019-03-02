---
title: MySQL定时弹出一个taskeng.exe
tags:
  - MySQL
  - 数据库
categories: 数据库
copyright: true
abbrlink: 53b2030c
date: 2018-02-27 20:47:08
password:
---

## 问题：

在使用电脑时，MySQL定时弹出一个taskeng.exe页面，过几秒后就自动关闭，页面内容如下：
```
=================== Start Initialization ===================
MySQL Installer is running in Community mode

Initializing product requirements
Loading product catalog
Checking for product catalog snippets
Checking for product packages in the bundle
Categorizing product catalog
Finding all installed packages.

```
但是电脑上并没有运行任何MySQL库

## 解决办法：

这个是新版本MySQL服务自带的一个定时任务，定时执行的任务，我们只需要在本地系统的“任务计划程序”中将这个定时任务干掉就OK了。

以win10为例：
在小娜中搜索任务计划程序：
 ![ ][1]
打开任务计划程序库，找到`MySQLNotifierTask`禁用就行了
 ![][2]

温馨提示：尽量不要直接删掉这个MySQL定时服务器，如果到后期需要扩张的时候，还能用到，可以仿照到这个进行定时任务的创建工作，这个是非常实用的。



  [1]: http://data.singlelovely.cn/xsj/20182/1518408796053.jpg
  [2]: http://data.singlelovely.cn/xsj/20182/1518408922003.jpg