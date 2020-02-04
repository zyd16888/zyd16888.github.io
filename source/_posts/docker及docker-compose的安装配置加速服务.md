---
title: docker及docker-compose的安装配置加速服务
copyright: true
abbrlink: bc197637
notshow: false
tags:
  - docker
categories: docker
description: 使用阿里云为docker加速
image:
  - 'https://data.singlelovely.cn/images/20200204225029.jpg!CoverPicture'
date: 2020-02-04 22:47:00
password:
photos:
sticky:
---

本文系统全部以`Ubuntu18.04 Service`为例

### docker安装

最近在服务器上部署应用，使用docker比较多，毕竟管理起来方便，腾讯云官方镜像已经默认换了腾讯的源，安装起来还可以，华为云的还是默认的源，下载速度非常不稳定。

最先试的是把腾讯云的源直接拷贝到华为的机器这边，然后发现更不更新不了，直接就断开链接了，推测是腾讯那边作了鉴权啥的，然后换网上搜到的源，发现好多文章的源列表并不是完全的(或者更新不及时)，只是一部分，安装`docker`的时候会提示找不到包。

这里附上清华的[开源镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)

安装教程建议使用[官方文档](https://docs.docker.com/install/linux/docker-ce/ubuntu/)，以免出问题。

### docker-compose安装

首先放上[官方文档](https://docs.docker.com/compose/install/)

因为某些原因，国内速度比较慢，运气不好的时候还会直接失败，以下为镜像地址：

地址来自[DaoCloud](https://get.daocloud.io/#install-compose)

```
curl -L https://get.daocloud.io/docker/compose/releases/download/1.25.4/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

### 配置加速服务

这里选用阿里云的容器镜像加速器：[点击进入](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)

按照操作文档配置就可以了

下面为Ubuntu的配置方式

1. 安装／升级Docker客户端
推荐安装1.10.0以上版本的Docker客户端，参考文档 docker-ce

2. 配置镜像加速器
针对Docker客户端版本大于 1.10.0 的用户

您可以通过修改daemon配置文件/etc/docker/daemon.json来使用加速器

```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://xxxxx.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

注意：因每个人的加速地址不同，所以上文中用xxxxx代替。