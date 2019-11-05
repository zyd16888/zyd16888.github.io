---
title: 中国大学mooc视频下载
copyright: true
abbrlink: '63840324'
tags:
categories:
date: 2018-05-31 17:08:52
password:
---

{% meting "1803053391" "xiami" "song"  "mutex:false" "listmaxheight:340px" "preload:none" "theme:#ad7a86"%}

   考试前准备突击一下，就看上了mooc的视频，视频是不错，但是官网并没有提供下载，学校也不是啥时候都有网，就想着把他下载下来，首先在电脑的浏览器里面抓了一下包，发现可以抓到视频，也可以下载，但一个一个手动下载太慢了，折腾了半天发现我水平有限，没法能批量获取到下载地址。
   ![ ](https://data.singlelovely.cn/xsj/2018/5/31/mooc1.png)
   然后就考虑到了手机端app，也试着抓了一下包，很容易的就发现了一个post请求了一个很长的json字符串，粗略的看一下，视频下载地址来了，还有不同的清晰度。
   ![ ](https://data.singlelovely.cn/xsj/2018/5/31/mooc2.png)
   
   接下来的事情就简单了，用python写一个脚本，把所有的视频下载就好了
   ```python
   
  # coding: utf-8
import json
import os
import urllib.request
jsonFile=open('json.txt' ,encoding='UTF-8').read()#事先将抓包所得的json保存为同目录下的文本文件
jsonObj=json.loads(jsonFile)
def Schedule(a,b,c):#下载进度指示

    """
    a:已经下载的数据块
    b:数据块的大小
    c:远程文件的大小
    """

    
    per = 100.0 * a * b / c  
    if per > 100 :  
        per = 100  
    print('%.2f%%' % per)  
def getMOOCLessons(jsonObj):  
    courseName=jsonObj['results']['courseDto']['name']+" "+jsonObj['results']['courseDto']['schoolName']  
    os.mkdir(courseName)#创建名称为“课程名+校名”的根目录  
    chapters=jsonObj['results']['termDto']['chapters']#读取所有章节的信息为一个列表  
    for i in range(len(chapters)):#遍历所有章节  
        os.mkdir(courseName + '\\' + chapters[i]['name'])#每一个章节建立一个文件夹  
        print(chapters[i]['name'])  
        lessons=chapters[i]['lessons']#读取当前章节下所有课时的信息为一个列表  
        for j in range(len(lessons)):#遍历所有课时  
            units=lessons[j]['units']#读取当前课时下所有小节的信息为一个列表  
            for k in range(len(units)):#遍历所有小节  
                aunit=units[k]  
                if (aunit["contentType"]==1):#判断该小节是否为视频内容  
                    print("Downloading "+aunit['name'])  
                    urllib.request.urlretrieve(aunit["resourceInfo"]["videoSHDUrl"], courseName + '\\' + chapters[i]['name']+'\\'+aunit['name']+".mp4", Schedule)#下载文件，这里下载的是高清资源
getMOOCLessons(jsonObj)  
   ```
   
需要的支持库：request模块

来看看下载好的结果
![ ](https://data.singlelovely.cn/xsj/2018/5/31/mooc3.png)

