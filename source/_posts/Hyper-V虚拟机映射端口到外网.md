---
title: Hyper-V虚拟机映射端口到外网
copyright: false
abbrlink: 56435b42
notshow: false
description: 端口映射
image:
  - 'https://data.singlelovely.cn/CoverPicture/56435b42.jpg!CoverPicture'
date: 2020-12-21 13:21:00
tags:
- 网络
- 虚拟机
categories: 网络
password:
photos:
sticky:
---

Hyper-V中创建虚拟机后，可以连接虚拟交换机，通过虚拟交换机连接到物理机

但虚拟机如果有端口需要对外提供服务时，外部网络只能访问到物理机，无法访问到虚拟交换机的网络

此时则可以使用`[netsh](https://docs.microsoft.com/zh-cn/windows-server/networking/technologies/netsh/netsh)`将虚拟机网络端口映射到物理机

<span id="inline-purple">添加端口转发</span>

比如使用IPv4+Port访问转发到IPv4+Port访问,就使用

netsh interface portproxy add v4tov4 listenaddress=监听IP listenport=监听端口 connectport=目标端口 connectaddress=目标IP

其中listenaddress可以省略,省略后就会监听所有访问物理机的IP,就不用担心网络环境改变后物理机的IP改变需要重新设置的问题

比如我想外部访问80端口,转发到虚拟机的172.17.89.39:80,则命令如下(不指定IP时则监听所有IP)：

```
netsh interface portproxy add v4tov4 listenport=80 connectport=80 connectaddress=192.168.147.199
```

<span id="inline-purple">删除端口转发</span>

比如我要删除一个v4tov4的端口转发,就使用

netsh interface portproxy delete v4tov4 listenaddress=监听IP listenport=监听端口

如果你的监听IP设置的泛型,删除也不用填

比如我要删除上述添加的转发规则,命令就是

```
netsh interface portproxy delete v4tov4 listenport=80
```

<span id="inline-purple">查看所有转发规则</span>

使用如下命令

```
netsh interface portproxy show all
```

当然如果你只想看v4tov4

就把最后改为v4tov4

```
netsh interface portproxy show v4tov4
```