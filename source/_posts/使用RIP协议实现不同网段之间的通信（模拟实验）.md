---
title: 使用RIP协议实现不同网段之间的通信（模拟实验）
tags:
  - eNSP
  - ICT
  - 数据通信
categories: 网络
copyright: true
abbrlink: 6d7b9178
date: 2018-03-24 23:38:14
password:
---

### 实验目标
+  使用RIP协议实现不同网段之间的通信
+  熟练RIP协议的路由配置过程
+  加深对vlan技术的理解

### 实验工具

 eNSP模拟器（510版）
 
 ### 网络拓扑图
 
 ![RIP网络拓扑图][1]
 
 ### 主要设备配置

<font color=#00FFFF >注：以下为设备的配置状态，并非配置命令</font>

#### LSW1
```
#
sysname ZYDSW1
#
vlan batch 10 12 20 30
#
cluster enable
ntdp enable
ndp enable
#
drop illegal-mac alarm
#
diffserv domain default
#
drop-profile default
#
aaa 
 authentication-scheme default
 authorization-scheme default
 accounting-scheme default
 domain default 
 domain default_admin 
 local-user admin password simple admin
 local-user admin service-type http
#
interface Vlanif1
#
interface Vlanif10
 ip address 192.168.1.1 255.255.255.0 
#
interface Vlanif12
 ip address 192.168.12.2 255.255.255.0 
#
interface Vlanif20
 ip address 192.168.2.1 255.255.255.0 
#
interface Vlanif30
 ip address 192.168.3.1 255.255.255.0 
#
interface MEth0/0/1
#
interface GigabitEthernet0/0/1
 port link-type access
 port default vlan 12
#
interface GigabitEthernet0/0/2
 port link-type access
 port default vlan 10
#
interface GigabitEthernet0/0/3
 port link-type access
 port default vlan 20
#
interface GigabitEthernet0/0/4
 port link-type access
 port default vlan 30
#
interface NULL0
#
rip 1
 undo summary
 version 2
 network 192.168.1.0
 network 192.168.2.0
 network 192.168.3.0
 network 192.168.12.0
#
user-interface con 0
user-interface vty 0 4
#
port-group default
#
return 

```
#### R2
```
#
sysname ZYDR2
#
aaa 
 authentication-scheme default
 authorization-scheme default
 accounting-scheme default
 domain default 
 domain default_admin 
 local-user admin password cipher OOCM4m($F4ajUn1vMEIBNUw#
 local-user admin service-type http
#
firewall zone Local
 priority 16
#
interface Ethernet0/0/0
 ip address 192.168.13.2 255.255.255.0 
#
interface Ethernet0/0/1
 ip address 192.168.12.1 255.255.255.0 
#
interface Serial0/0/0
 link-protocol ppp
#
interface Serial0/0/1
 link-protocol ppp
#
interface Serial0/0/2
 link-protocol ppp
#
interface Serial0/0/3
 link-protocol ppp
#
interface GigabitEthernet0/0/0
#
interface GigabitEthernet0/0/1
#
interface GigabitEthernet0/0/2
#
interface GigabitEthernet0/0/3
#
wlan
#
interface NULL0
#
rip 1
 undo summary
 version 2
 network 192.168.13.0
 network 192.168.12.0
#
user-interface con 0
user-interface vty 0 4
user-interface vty 16 20
#
return 
```
#### R1
```

#
sysname ZYDR1
#
aaa 
 authentication-scheme default
 authorization-scheme default
 accounting-scheme default
 domain default 
 domain default_admin 
 local-user admin password cipher OOCM4m($F4ajUn1vMEIBNUw#
 local-user admin service-type http
#
firewall zone Local
 priority 16
#
interface Ethernet0/0/0
 ip address 192.168.13.1 255.255.255.0 
#
interface Ethernet0/0/1
 ip address 192.168.24.1 255.255.255.0 
#
interface Serial0/0/0
 link-protocol ppp
#
interface Serial0/0/1
 link-protocol ppp
#
interface Serial0/0/2
 link-protocol ppp
#
interface Serial0/0/3
 link-protocol ppp
#
interface GigabitEthernet0/0/0
#
interface GigabitEthernet0/0/1
#
interface GigabitEthernet0/0/2
#
interface GigabitEthernet0/0/3
#
wlan
#
interface NULL0
#
rip 1
 undo summary
 version 2
 network 192.168.13.0
 network 192.168.24.0
#
user-interface con 0
user-interface vty 0 4
user-interface vty 16 20
#
return 
```
R3与R2配置类似，LSW2与LSW1类似

#### 主机配置示例
![主机配置示例][2]

### 结果测试

![ ][3]
![ ][4]


  [1]: http://data.singlelovely.cn/xsj/2018/3/24/RIP%E7%BD%91%E7%BB%9C%E6%8B%93%E6%89%91%E5%9B%BE.png
  [2]: http://data.singlelovely.cn/xsj/2018/3/25/%E4%B8%BB%E6%9C%BA%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B.png
  [3]: http://data.singlelovely.cn/xsj/2018/3/25/%E7%BB%93%E6%9E%9C%E6%B5%8B%E8%AF%95.png
  [4]: http://data.singlelovely.cn/xsj/2018/3/25/%E7%BB%93%E6%9E%9C%E6%B5%8B%E8%AF%952.png