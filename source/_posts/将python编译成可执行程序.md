---
title: 将python编译成.exe可执行程序
copyright: true
abbrlink: a044f431
notshow: false
tags:
  - python
categories: python
description: 使用pyinstaller
date: 2019-05-22 17:01:00
password:
image:
- "http://data.singlelovely.cn/CoverPicture/a044f431.jpg"
photos:
sticky:
---

在将java程序打包成可执行程序后，因为运行时需要jvm虚拟机，还是没有办法直接给别人用，网上查了半天没有找到解决方法。最后决定用python将整个程序重写一遍，然后打包。

在此记录一下python打包的流程。

## 安装pyinstaller

```python
pip install pyinstaller
```

如果有 ~\Scripts 文件夹的环境变量的，应该可以直接使用，没有的配置一下环境变量可以了

## 使用方法

```python
pyinstaller -F xxxx.py
```

-F 的作用是打包为单文件

更多命令参数请参阅：[官方文档](https://pyinstaller.readthedocs.io/en/stable/usage.html)