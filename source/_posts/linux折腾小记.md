---
title: linux折腾小记
copyright: true
abbrlink: 5fdb7ae9
notshow: false
description: 用户、shell、oh-my-zsh、systemd、磁盘
image:
  - 'https://data.singlelovely.cn/CoverPicture/c6360c4.png!CoverPicture'
date: 2020-02-21 23:28:00
tags:
- Linux
categories: Linux
password:
photos:
sticky:
---

主要记录一下最近在服务器上遇到的问题及解决办法，以便事后查找，以免忘记。

## 用户

### 创建

一把梭：

```
sudo useradd -r -m -s /bin/bash username
```

- -r：建立系统账号
- -m：自动建立用户的登入目录
- -s：指定用户登入后所使用的shell

正常方式：

```
sudo adduser username
```

这种方式创建的用户，登陆以后只要一个$，没有显示用户名和路径。

查看 `/etc/passwd` 后发现，新建的用户未指定 shell，需要指定一下
```
sudo usermod -s /bin/bash username
```

### 授权

编辑 `/etc/sudoers` 文件，root 用户可以直接编辑，其他用户使用以下命令授权
```diff
+ sudo chmod u+w /etc/sudoers  授权
- sudo chmod u-w /etc/sudoers  撤销
```
然后增加以下行（按需添加）
```
youuser            ALL=(ALL)                ALL
%youuser           ALL=(ALL)                ALL
youuser            ALL=(ALL)                NOPASSWD: ALL
%youuser           ALL=(ALL)                NOPASSWD: ALL
```

1. 允许用户youuser执行sudo命令(需要输入密码).
2. 允许用户组youuser里面的用户执行sudo命令(需要输入密码).
3. 允许用户youuser执行sudo命令,并且在执行的时候不输入密码.
4. 允许用户组youuser里面的用户执行sudo命令,并且在执行的时候不输入密码.

### 改密

- passwd `username`

### 删除

1. `sudo userdel username`
2. `sudo rm -rf /home/username`
3. 删除或者注释掉`/etc/sudoers`中关于要删除用户的配置。

- `sudo deluser --remove-home username`
- `sudo deluser -r username`

## oh-my-zsh

### 安装 zsh

```
sudo apt install zsh
zsh --version
```

### 安装 oh-my-zsh

参考 ： https://github.com/nianxiongdi/oh-my-zsh

### 插件

```shell ~/.zshrc
#zhs的主题
ZSH_THEME="ys"

#z命令快速跳转目录     x命令解压一切文件
plugins=(
    git z zsh-autosuggestions extract web-search zsh-syntax-highlighting
)

#自动补全插件
source ~/.oh-my-zsh/plugins/incr/incr.zsh
```

`zsh-autosuggestions`与`zsh-syntax-highlighting`需手动安装

地址：[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)、[zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

### 自动部署

计划中。。。

## systemd

[参考](https://blog.csdn.net/weixin_37766296/article/details/80192633)

## 磁盘



## nohup &

nohup: 加在一个命令的最前面，表示不挂断的运行命令

&: 加载一个命令的最后面，表示这个命令放在后台执行

### 查看后台运行的命令

- jobs
- pa

例：`ps -aux|grep python`

  - a: 显示所有程序
  - u: 以用户为主的格式来显示
  - x: 显示所有程序，不以终端机来区分

### 关闭后台运行的程序

`kill %pid`

### 前后台进程的切换与控制

- fg
  - 将后台中的命令调至前台继续运行
  -  fg %pid
- Ctrl + z
  - 将一个正在前台执行的命令放到后台，并且处于暂停状态
- bg
  - 将一个在后台暂停的命令，变成在后台继续执行
  - bg %pid
