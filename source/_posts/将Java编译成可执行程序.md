---
title: 将Java编译成.exe可执行程序
copyright: true
abbrlink: 5f85a932
notshow: false
tags:
  - Java
  - 学习
  - 教程
categories: Java
description: 使用idea与exe4j（多图）
date: 2019-05-22 09:42:00
password:
image:
- "http://data.singlelovely.cn/CoverPicture/5f85a932.jpg"
photos:
sticky:
---

## 将Java源代码打包成jar包

以`idea`为例，打开`项目结构`(Ctrl+Alt+Shift+S)，选择`Artifacts`，点击加号，选择jar from modules with dependencis...

![图一](https://data.singlelovely.cn/images/20190522091006.png)
![图二](https://data.singlelovely.cn/images/20190522091120.png)

然后选择`构建`->`构建项目`，便会在out文件夹下生成编译后的jar包

![图三](https://data.singlelovely.cn/images/20190522091415.png)

## 将jar包打包生成.exe文件

首先安装`exe4j`软件，然后按以下步骤执行

![1](https://data.singlelovely.cn/images/20190522091750.png)
![2](https://data.singlelovely.cn/images/20190522091931.png)
![3](https://data.singlelovely.cn/images/20190522092120.png)
![4](https://data.singlelovely.cn/images/20190522092607.png)
![5](https://data.singlelovely.cn/images/20190522092317.png)
![6](https://data.singlelovely.cn/images/20190522093002.png)
![7](https://data.singlelovely.cn/images/20190522093359.png)

接下来，一直点下一步，直到打包完成。

然后测试是否能够正常运行。

## 报错常见问题

- jre目录路径设置不正确（注意相对路径）
- 32与64位和当前系统不对应
- 打包程序输出类型选择不正确

## 附

exe4j ：[下载地址](https://exe4j.apponic.com/) (官方)

exe4j,未注册版本会在程序开始提示程序由exe4j打包生成。

exe4j注册码
```
用户名和公司名可随便填
A-XVK258563F-1p4lv7mg7sav

A-XVK209982F-1y0i3h4ywx2h1

A-XVK267351F-dpurrhnyarva

A-XVK204432F-1kkoilo1jy2h3r

A-XVK246130F-1l7msieqiwqnq

A-XVK249554F-pllh351kcke50
```