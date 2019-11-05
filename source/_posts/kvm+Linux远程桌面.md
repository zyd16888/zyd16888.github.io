---
title: Linux系统的vps（kvm架构）安装vnc
tags: vps
categories: vps
copyright: true
abbrlink: 30631cd4
date: 2018-02-06 20:47:08
password:
---

&emsp; &emsp;vps服务商提供的系统一般是不带图形化界面的（Ubuntu部分会有），但有时有些软件必须要图形化界面才能操作，所以需要手动安装vnc，通过vnc实现图形化界面的访问。

&emsp; &emsp;目前大多数的一键安装包都是基于ovz架构的vps，kvm架构的由于不能直接安装XFCE，会提示找不到数据源，需要通过其他方法实现。

`本教程使用 搬瓦工的Centos 6 x86_64 系统，其他系统自测`

### 准备工作
1、安装Centos 6 64位系统，最好是自带bbr的，速度会更高。
![][1]
2、使用终端模拟软件连接vps，推荐使用SecureCRT或者Xshell5。
### 可视化桌面安装

#### 升级系统和安装图形界面
依次执行下面代码：
```
yum -y update
yum groupinstall "Desktop" -y
```
#### 安装Tight VNC
```
yum install tigervnc-server -y
```
#### 创建用户
```
adduser vncuser

su vncuser
vncpasswd
```
`vncpasswd`输入后会提示输入密码，并确认。
然后输入`su root`以回到root账户下，回到root账户时会要求输入root密码。

#### 设置连接端口和分辨率
输入
```
vi /etc/sysconfig/vncservers
```
键盘上点击I键进入编辑模式，在文件最后添加（分辨率自己调节）
```
VNCSERVERS="2:vncuser"
VNCSERVERARGS="-geometry 1080×1920"
```
![][2]
然后输入`:wq`保存并退出

#### 启动vnc并设置开机自启
启动vnc，重启将start改为restart即可
```
service vncserver start
```
设置开机自启
```
chkconfig vncserver on
```
### 连接远程桌面
打开vnc客户端，输入`服务器地址:1`例如`104.207.128.86:1`,然后输入密码就可以看到远程桌面了
![][3]


&emsp; &emsp;有了远程桌面以后么，就可以干一些挂机等在终端界面无法操作的事情啦········

  [1]: https://data.singlelovely.cn/xsj/20182/@%5DV0D9K8Y%7BTOL3LD6%28~UWDM.png
  [2]: https://data.singlelovely.cn/xsj/20182/%5BU4HMPKB9TOC1%5BN8%2809IQPL.png?75|imageslim
  [3]: https://data.singlelovely.cn/xsj/20182/37N0~QI8JIR@4BL32IGWDTT.png?75|imageslim