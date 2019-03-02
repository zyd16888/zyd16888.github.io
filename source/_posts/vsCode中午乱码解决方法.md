---
title: VS code 显示中文异常解决办法
copyright: true
abbrlink: fdf0e152
date: 2018-06-28 23:28:36
tags:
categories:
password:
---

{% meting "1803360770" "xiami" "song"  "mutex:false" "listmaxheight:340px" "preload:none" "theme:#ad7a86"%}

从https://www.zhihu.com/question/34415763得到问题解决办法，现做如下总结。

异常原因：VSCODE默认是UTF-8编码打开文件的。如果遇到了像GB18030 GBK等等的编码，就显示乱码了。

解决办法如下：

1，一劳永逸法：

 在设置文件中加入： <font color=#1a237e>"files.autoGuessEncoding":true</font>
，自动识别字符编码。

 ps：a:此设置可能需要最新版本的VScode，因为我当前用的就是最新版，所以修改后显示马上正常了。
 &emsp; &emsp;b:设置文件打开位置：文件--.>首选项-->设置-->用户设置。

2，单个文件解决办法：

 vs code界面右下角位置有显示解析当前文件所用的字符源码（默认是UTF-8），单击该处,手动更改编码
 
 3，vscode默认文件字符编码为utf-8，可以在用户设置修改该属性，如：files.encoding"："gbk"