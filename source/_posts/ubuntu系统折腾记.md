---
title: Ubuntu系统折腾记
copyright: true
abbrlink: 1a300c2b
notshow: false
tags:
  - Ubuntu
  - Linux
categories: 系统
description: 美化和必备软件安装
date: 2019-02-17 19:54:00
password:
image:
- "https://data.singlelovely.cn/CoverPicture/1a300c2b.png!CoverPicture"
photos:
sticky:
---

## 换源

Ubuntu18.04国内版默认的源地址为 cn.archive.ubuntu.com ， ping结果显示归属地为英国，速度较慢，需要更换为国内的镜像地址。
使用如下命令：

```shell
//得到系统版本代号，防止更换错误
lsb_release -c  

//备份原有源
cp /etc/apt/sources.list /etc/apt/sources.list.backup
```

清华大学镜像站： https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/

阿里源

```js
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
```

更换完成后执行

```shell
sudo apt-get update
sudo apt-get upgrade
```

## 安装<span id="font-red">ssr</span>

桌面客户端下载：[地址](https://github.com/erguotou520/electron-ssr)

参考：[教程](https://alanlee.fun/2018/05/18/ubuntu-ssr/)

安装libsodium，用来支持chacha20系列加密方式

```bash
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/libsodium.sh && chmod +x libsodium.sh && bash libsodium.sh
```

~~脚本来源：[逗比根据地](https://doubibackup.com/)~~

注意：装完libsodium后需要重启系统

## 安装必备软件

国外公司对Linux系统的支持还是比较好的，vscode、chrome等去官网下载deb包安装就行了

## 安装国内软件

国内的一些常用软件，微信，QQ等对Ubuntu的支持并不友好，Ubuntu版维护停止在多年以前，大多数已经不能使用，网上多数解决办法是通过网页版，网页版界面不友好操作麻烦，在此使用deepin深度定制的wine安装包。

github地址： https://github.com/wszqkzqk/deepin-wine-ubuntu

教程及演示： https://www.lulinux.com/archives/1319

## 美化

### 终端及管理器安装

打开终端，查看shell版本

```shell
gnome-shell --version
```

如无gnome shell 使用下面命令安装

```shell
sudo apt install gnome-shell
```

然后安装 gnome-tweak 中文名为 优化

使用下面命令安装，或者在Ubuntu软件搜索<span id="inline-green">gnome-tweak</span>安装

```shell
sudo apt install gnome-tweak-tool
```
### gnome-tweak 插件安装

- 通过Ubuntu软件商店搜索安装
    - 速度较慢，不推荐此方法
- 通过[官网](extensions.gnome.org)下载
    - chrome浏览器需到应用商店安装 <span id="inline-green">GNOME Shell integration</span> 扩展程序
    - 火狐浏览器根据页面提示执行

### 推荐的插件

- User Themes: 作用是从用户目录加载主题
- Dash to Dock : 作用是制定Dock和Dash
    - 主题图标[下载](https://www.gnome-look.org/)
    - 主题目录：/usr/share/themes
    - sell主题目录：/usr/share/gnome-shell
    - 图标包目录：/usr/share/icons
- TopIcons Plus : 起到了任务栏的作用,用来解决上面wine程序任务栏图标问题
- Gnome-shell Extensions ：通过Ubuntu软件商店安装 插件集合，一次性安装多个常用插件

### 参考教程

[Ubuntu18.04美化及常用软件安装](https://blog.csdn.net/weixin_38233274/article/details/80782483)

[如何让Ubuntu美如画](https://www.youtube.com/watch?v=B6oCQit90M8)

[GNOME Shell 详细指南](https://linux.cn/article-9447-1.html?pr)

## 网易云的安装及踩坑

之所以要单独写一个网易云，实在是因为坑太多了，记录一下，以防万一

### 安装

去官网下载安装包，通过<span id="inline-blue">sudo dpkg -i</span>安装

```bash
sudo dpkg -i netease-cloud-music_1.1.0_amd64_ubuntu.deb
```

上面的操作可能会出错，一般来说就是依赖的软件环境不完整，执行以下命令

```bash
sudo apt-get -f install
```

### 启动

在软件中能看到网易云音乐的图标，可是点击运行之后却没有任何窗口出现。

通过终端进行启动

```bash
netease-cloud-music
```

发现报错并卡住

```bash
Gtk-Message: 12:02:46.607: Failed to load module "canberra-gtk-module"
```

安装相应依赖，不安装依赖通过 <span id="inline-blue">sudo netease-cloud-music</span> 也能启动，但是控制台会有报错信息

```bash
sudo apt-get install libcanberra-gtk*
```

结果安装依赖后还是得通过 <span id="inline-blue">sudo netease-cloud-music</span> 启动，并且不能关闭终端窗口

### 问题解决

以上方法虽然能够使网易云音乐运行，但每次都需要打开一个终端不能关闭，让有轻微强迫症的我看了觉得很不舒服。

<div class="note success">
<span id="font-blue">启动密籍：</span>双击网易云音乐图标后，点击关机，十秒内就出现界面（此方法实测可用）
</div>

方法2(请自行测试)：
在~目录下新建一个脚本<span id="inline-blue">.netease.sh</span>,该脚本的内容如下(注意更换password)：

```bash
#!/bin/bash
echo "password" | sudo -S netease-cloud-music &
sleep 0.1
exit
```

编辑~/.bashrc，在末尾增加了一行：

>alisa netease=". .netease.sh"

## deb包安装方式

- 双击打开安装
    - 通过Ubuntu自带的软件管理器安装
    - 容易出现依赖错误
    - 安装速度慢
    - 出错后报错信息不明确

- 通过命令 <span id="inline-blue">sudo dpkg -i</span> 安装

## 双系统下无法访问win磁盘问题

### 方法一

通过win系统重启进入ubuntu系统

### 方法二

执行以下命令,记得加磁盘分区号(如果执行前已挂载磁盘需要先卸载，执行完毕重新挂载即可)

```bash
sudo ntfsfix /dev/sda  or   sudo ntfsfix /dev/nvmeOn
```

## PPPoE 拨号上网

```bash
# 安装 pppoeconf
sudo apt install pppoeconf
# 配置
sudo pppoeconf
# 手动连接
sudo pon dsl-provider
# 手动断开
sudo poff dsl-provider
# 查看状态
sudo plog
# 查看接口信息
sudo ip addr show ppp0
```

注意：不适用于需要客户端的登陆方式，因为客户端一般都有二次验证