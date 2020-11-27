---
title: ZeroTier安装配置及路由下整个网段异地组网
copyright: false
abbrlink: 9611a2bf
notshow: false
description: ZeroTier实在是太好用了
image:
  - 'https://data.singlelovely.cn/images/20201127160513.png!CoverPicture'
date: 2020-11-27 13:36:00
tags:
categories:
password:
photos:
sticky:
---

`ZeroTier`是一个基于UDP的异地组网工具，支持多平台，开箱即用。首次连接需要与转发服务器通信，建立连接后，则直接在两个客户端间通过UDP通信。

## 下载安装

Linux下安装方式如下，其它系统可以参照官网：https://www.zerotier.com/download/

- 一键安装程序
```bash
curl -s https://install.zerotier.com/ | sudo bash
```

> 注意：此安装方式不适用于openwrt系统，openwrt可以直接安装ipk插件
> `opkg install zerotier`

## Moon转发节点配置

Linux服务器可以作为Moon节点，可以改善与`ZeroTier`官方服务器通信的延迟。

- 将VPS加入网络，需要在控制面板上同意

```shell
zerotier-cli join 网络ID
```

- 进入`zerotier-one`目录，生成配置文件

```bash
cd /var/lib/zerotier-one
zerotier-idtool initmoon identity.public > moon.json
```

- 修改moon.json文件

修改文件中的“stableEndpoints”为 VPS的IP地址及开放的端口号,例如“stableEndpoints: [“8.8.8.8/9993”]

- 生成签名文件

```bash
zerotier-idtool genmoon moon.json
```

- 在安装目录下创建一个moons.d的文件夹，并将000000xxxx.moon移入，并重启服务

```shell
service zerotier-one restart
```


## 客户端加入Moon节点

1. windows安装目录
   - C:\ProgramData\ZeroTier\One
2. linux安装目录
   - /var/lib/zerotier-one

在安装目录下创建一个moons.d文件夹，将签名文件放入，随后重启服务即可。

在命令行执行：`zerotier-cli listpeers`，如果有Moon节点标签，则连接成功


## 利用ZeroTier转发整个网段进行组网

ZeroTier会自动对安装了客户端的机器进行配置下发，在网站管理面板直接修改配置后，几分钟即可自动下发到客户端。


在某些情况下，网络中的设备，不一定支持安装zerotier客户端，或者多客户端管理起来比较麻烦，则可以在路由器上安装zerotier，然后将整个路由器下的设备进行异地组网。

> 需要zerotier虚拟局域网的网段与路由器lan下的网段不同，若多个路由的lan网段组网，需要每个路由下的lan网段不同。

如zerotier的虚拟网段为：10.147.17.*，给路由器分配的IP为10.147.17.10，路由器下lan的网段为192.168.1.0，则需要添加的路由为：192.168.1.0 via 10.147.17.10

![](https://data.singlelovely.cn/images/20201127160023.png)

添加路由后，等待几分钟（配置下发时间），即可在别的加入虚拟网络中的客户端，直接使用`192.168.1.*`地址访问路由器下的内网机器。


















