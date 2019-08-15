---
title: win10文件因继承权限等问题导致无法操作解决方案
copyright: false
abbrlink: c6360c4
notshow: false
tags:
  - 教程
  - windows
categories: 系统
description: 自己电脑上的东西怎能没有权限呢！！！
date: 2019-08-16 04:00:00
password:
image:
- "https://data.singlelovely.cn/CoverPicture/c6360c4.png!CoverPicture"
photos:
sticky:
---

首先吐槽一下win10的权限管理，个人感觉及其混乱，尤其是在重装系统以后，有些文件的权限就会莫名其妙的没有了，还有一些从网上下载的文件也会出现没有权限的情况，造成不能删除等问题。

以前出现这样的问题，去文件属性里面的安全选项卡，然后高级，启用一下继承，权限就来了，没有深究原因（又不是不能用）  实在不行还能进PE强行删文件嘛

这次是因为搞了个无损的原声带，想拷贝一下，结果有权限保护，一个一个的点属性太麻烦了，就上网找了一下，各种折腾半天没成功，最后花了点时间研究了下win10的权限管理，特此记录。

## 方式一

想获取整个文件夹内及其子文件的权限时，右键文件夹属性、安全选项卡，这个页面看一下那个组或用户名对文件具有完全控制的权限，然后高级、更改所有者，将所有者改为具有完全控制权限的用户（勾选替换子容器和对象的所有者），更改完成后登录具有权限的用户进行操作。

![01](https://data.singlelovely.cn/images/20190816034535.png)

![02](https://data.singlelovely.cn/images/20190816034710.png)

![03](https://data.singlelovely.cn/images/20190816034818.png)

## 方式二

粗暴简单，推荐使用此方法

cmd命令行（管理员模式），执行类似如下命令：

```shell
icacls "H:\音乐\五月天\步步自選作品輯 The Best of 1999-2013 [一路有你版] Disc 2\*.*" /grant Users:(F)
```

`"目录名"`

`*.*`  正则表达式

`Users`  用户组或者用户名

`(F)` 完全控制

![04](https://data.singlelovely.cn/images/20190816035552.png)

这样修改完权限以后就可以随便怎么用了
