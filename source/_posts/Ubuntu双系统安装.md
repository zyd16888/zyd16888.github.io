---
title: UEFI启动下，Win10+Ubuntu双系统安装
copyright: true
tags:
  - Ubuntu
  - Linux
  - uefi
categories: 系统
abbrlink: 65a05ef
date: 2018-01-29 08:38:39
---

**注意：**`Uefi启动只能使用Ubuntu引导，不能使用Win引导`


## 第一，分配空间
Linux没有什么C盘D盘的概念，只有分区挂载目录的概念，所以你在Windows下 `只需要分出一块较大的未分配空间就行，记住不要去格式化` ，保证其&quot;未分配&quot;属性(windows系统中看是黑色的)（Linux的文件系统和Win是不一样的，NTFS和FAT32都不适用）。

用Win自带的磁盘管理不能合并不相邻的未分配空间，所以你要想C盘割一点，D盘割一点，再合在一起那是不行的， `解决办法是在 使用分区助手合并，但比较耗费时间` 。

## 第二，制作安装盘
你必须要有一个U盘，然后使用软碟通或者USBWriter把iso系统镜像文件烧录进去，这是比较传统的方法， UEFI启动，不需要刻录工作了， `直接将iso里的所有文件解压至U盘即可` 。

然后 `关闭Windows的快速启动` ，重启电脑，进入BIOS后， `关闭Security Boot`（部分电脑没有这一项，就不用管了），最后 `选择UEFI下的U盘启动`

## 第三，安装系统
选中USB启动，回车后即进入Ubuntu安装流程，按照正常的步骤， `如果你选择了安装更新和第三方软件，那么一定要记得联网，否则会卡死在最后的进度条上，所以最好不要勾选。另外，不要选择"与其它系统共存";那一项，而选择最后那个"其它选项"（创建自己的分区）。`

## 第四，Ubuntu分区挂载（重要）
1. **swap交换空间** ，这个也就是虚拟内存的地方，选择 `主分区` 和 `空间起始位置` 。如果你给Ubuntu系统分区容量足够的话，最好是能给到你 `物理内存的2倍`大小
2. 新建 **efi系统分区** ，选中 `逻辑分区` 和 `空间起始位置` ，大小最好不要小于256MB，系统引导文件都会在里面，它的作用和boot引导分区一样，但是boot引导是默认grub引导的，而efi是UEFI引导的。 也就是最后的挂载点里没有&quot;/boot&quot;这一项 ，否则就没办法UEFI启动两个系统了。
3. **挂载&quot;/home&quot;** ，类型为 `EXT4日志文件系统` ，选中 `逻辑分区` 和 `空间起始位置` ，这个相当于你的个人文件夹，类似Windows里的User，总的来说， `最好不要低于8GB` 。
&emsp;&emsp;（这里特别提醒一下，Ubuntu最新发行版不建议强制获取Root权限，因为我已经玩崩过一次。所以你以后很多文档、图片、包括免安装软件等资源不得不直接放在home分支下面。你作为图形界面用户，只对home分支有完全的读写执行权限，其余分支例如usr你只能在终端使用sudo命令来操作文件，不利于存放一些直接解压使用的免安装软件。因此，建议home分支多分配一点空间，……）
4. **挂载&quot;/usr&quot;** ，类型为 `EXT4日志文件系统` ，选中 `逻辑分区` 和 `空间起始位置` ，这个相当于软件安装位置，Linux下一般来说安装第三方软件你是没办法更改安装目录的，系统都会统一地安装到/usr目录下面，因此，这个分区必须要大。
5. 最后， **挂载&quot;/&quot;** ，类型为 `EXT4日志文件系统` ，选中 `逻辑分区` 和 `空间起始位置` ，因为除了home和usr还有很多别的目录，但那些都不是最重要的，&quot;/&quot;就把除了之前你挂载的home和usr外的全部杂项囊括了， `大小也不要太小` ，最好不低于16GB。
&emsp; &emsp;如果你非要挨个仔细分配空间，那么你需要知道这些各个分区的含义（ [Linux(ubuntu)分区挂载点介绍](http://blog.sina.com.cn/s/blog_5f0a505101017ruf.html)）不过就算你把所有目录都自定义分配了空间也必须要给&quot;/&quot;挂载点分配一定的空间。

## 安装完成
安装成功后，会提示你拔掉U盘并且重启，重启后记得进入BIOS改回UEFI Security Boot On模式，也就是重新开启Security Boot，然后再重启你就可以看到选择系统的启动引导界面了，一般来说：
```
第一个是Ubuntu，选这个进入Ubuntu系统，
第二个是Ubuntu高级选项，
第三个是Windows Boot Manager，也就是启动你的Win10
```
## 更改默认启动项
安装windows和ubuntu双系统以后，默认启动变成ubuntu了，对那些经常要进windows的童鞋，每次开机都得按几次向下的箭头，再敲回车，非常不方便，这时就需要将默认启动改为Win10系统。

 打开ubuntu系统以后，打开超级终端，输入以下命令
 ```
 sudo gedit /etc/default/grub   #注意空格不能少
 ```
这时会打开cfg.文件，显示如下
```
# If you change this file, run &#39;update-grub&#39; afterwards to update
# /boot/grub/grub.cfg.
# For full documentation of the options in this file, see:
#   info -f grub -n &#39;Simple configuration&#39;

GRUB\_DEFAULT=0   
#GRUB\_HIDDEN\_TIMEOUT=0
GRUB\_HIDDEN\_TIMEOUT\_QUIET=true
GRUB\_TIMEOUT=10       
GRUB\_DISTRIBUTOR=`lsb_release -i -s 2&gt; /dev/null || echo Debian`
GRUB\_CMDLINE\_LINUX\_DEFAULT=&quot;quiet splash&quot;
GRUB\_CMDLINE\_LINUX=&quot;locale=zh\_CN&quot;
```
GRUB\_DEFAULT   &emsp;代表的就是启动项的顺序，从数字0开始，        
GRUB\_TIMEOUT   &emsp;代表选择界面停留时间

然后在终端依次运行命令：
```
sudo update-grub
reboot
```
重启电脑，默认启动的系统就换到windows了。

# 附1：

默认的Ubuntu启动引导界面可能有点丑，可以更换为第三方启动引导

如：rEFind：非常好的解决了uefi模式下win10与linux双系统引导菜单丢失的情况,它本身跨平台，有win，linux，mac版本，下载地址（官方）： [http://www.rodsbooks.com/refind/](http://www.rodsbooks.com/refind/)   

教程：  http://tieba.baidu.com/p/4380168027



# 附2：

传统BIOS引导教程（[使用EasyBCD管理启动项][1]）


  [1]: http://blog.csdn.net/zr459927180/article/details/51627910