---
title: 搭建ftp服务器并映射到外网（实验）
tags:
  - eNSP
  - ICT
  - 数据通信
categories: 网络
copyright: true
abbrlink: 74b1112a
date: 2018-03-25 16:41:56
password:
---

### 实验目标
+  使用RIP协议实现不同网段之间的通信
+  FTP服务器的搭建
+  学习NAT协议的的使用
+  内网IP映射到公网

### 实验工具

 eNSP模拟器（510版）
 
 ### 网络拓扑图
![网络拓扑图][1]

### 主要命令
 **AR**
```AR
interface GigabitEthernet0/0/0
ip address 192.168.21.1 255.255.255.0 
interface GigabitEthernet0/0/1
ip address 192.168.13.1 255.255.255.0
interface GigabitEthernet0/0/2
ip address 61.67.1.1 255.255.255.0 
nat server protocol tcp global 61.67.1.5 ftp inside 192.168.4.2 ftp
nat outbound 2000
rip 1
 undo summary
 default-route originate
 version 2
 network 192.168.21.0
 network 192.168.13.0
```
 **R3**
```R3
interface Ethernet0/0/0
 ip address 192.168.12.1 255.255.255.0
interface Ethernet0/0/1
 ip address 192.168.21.2 255.255.255.0
rip 1
 undo summary
 version 2
 network 192.168.12.0
 network 192.168.21.0
```
 **LSW1**
```LSW1
vlan batch 10 12 20
#
cluster enable
ntdp enable
ndp enable
#
drop illegal-mac alarm
#
dhcp enable
#
rip 1
 undo summary
 version 2
 network 192.168.1.0
 network 192.168.2.0
 network 192.168.12.0
#
interface GigabitEthernet0/0/1
 port link-type access
 port default vlan 10
#
interface GigabitEthernet0/0/3
 port link-type access
 port default vlan 12
#
interface GigabitEthernet0/0/2
 port link-type access
 port default vlan 20
```

### 主要配置
#### AR1
![1][2]
![2][3]
![3][4]
#### LSW1
![LSW1][5]
#### R1
![R1][6]
#### R2
![R2][7]
#### R3
![R3][8]

### 测试效果

![ ][9]
![ ][10]


  [1]: http://data.singlelovely.cn/xsj/2018/3/25/%E6%8B%93%E6%89%91%E5%9B%BE.png
  [2]: http://data.singlelovely.cn/xsj/2018/3/25/AR1.png
  [3]: http://data.singlelovely.cn/xsj/2018/3/25/AR2.png
  [4]: http://data.singlelovely.cn/xsj/2018/3/25/AR3.png
  [5]: http://data.singlelovely.cn/xsj/2018/3/25/LSW1.png
  [6]: http://data.singlelovely.cn/xsj/2018/3/25/R1.png
  [7]: http://data.singlelovely.cn/xsj/2018/3/25/R2.png
  [8]: http://data.singlelovely.cn/xsj/2018/3/25/R3.png
  [9]: http://data.singlelovely.cn/xsj/2018/3/25/%E5%AE%A2%E6%88%B7%E7%AB%AF.png
  [10]: http://data.singlelovely.cn/xsj/2018/3/25/%E7%BB%93%E6%9E%9C%E6%B5%8B%E8%AF%95.png