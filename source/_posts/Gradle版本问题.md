---
title: 'Could not find com.android.tools.build:gradle:3.0.0'
tags:
  - Android
  - 学习
categories: Android
copyright: true
abbrlink: 5133767d
date: 2018-03-02 20:47:08
password:
---

今天更新了Android Studio版本后，运行以前的项目时突然出现了下面的错误：
`Searched in the following locations:
    file:/G:/Android/Android Studio/gradle/m2repository/com/android/tools/build/gradle/3.0.0/gradle-3.0.0.pom
    file:/G:/Android/Android Studio/gradle/m2repository/com/android/tools/build/gradle/3.0.0/gradle-3.0.0.jar
    https://jcenter.bintray.com/com/android/tools/build/gradle/3.0.0/gradle-3.0.0.pom
    https://jcenter.bintray.com/com/android/tools/build/gradle/3.0.0/gradle-3.0.0.jar
Required by:
    project :
<a href="add.google.maven.repository">Add Google Maven repository and sync project</a><br><a href="openFile:C:\\Users\\dong\\AndroidStudioProjects\\PraClock-master-333c8464e4a6120e4a7c8235a11d5670005296dc\\build.gradle">Open File</a>
`
按照提示路径找到文件位置G:/Android/Android Studio/gradle/m2repository/com/android/tools/build/gradle
![][1]

发现是没有3.0.0的gradle造成的
找到项目中的gradle文件，将下面的位置更改即可
![][2]

然后点击sync或者try again刷新一下，问题解决。




  [1]: https://data.singlelovely.cn/xsj/20182/NDGcPRDMONQ53NVOKVA2K.png
  [2]: https://data.singlelovely.cn/xsj/20182/7OX%29OQX2%5B9_G%7BO2NI8F9E15.png