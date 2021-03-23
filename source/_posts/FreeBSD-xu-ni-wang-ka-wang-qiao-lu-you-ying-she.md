---
title: FreeBSD 虚拟网卡 网桥 路由 映射
date: 2021-03-23 13:52:49
tags:
---

#   网关与路由

netstat -r  
Routing tables  #路由表
Destination      Gateway            Flags     Refs     Use     Netif Expire
目的地            网关               状态                       接口   超时

U	Up	路由处于活动状态。
H	Host	路由目标是单个主机。
G	Gateway	所有发到目的地的网络传到这一远程系统上，并由它决定最后发到哪里。
S	Static	这个路由是手工配置的，不是由系统自动生成的。
C	Clone	生成一个新的路由， 通过这个路由我们可以连接上这些机子。 这种类型的路由通常用于本地网络。
W	WasCloned	指明一个路由――它是基于本地区域网络 (克隆) 路由自动配置的。
L	Link	路由涉及到了以太网硬件。

#   默认路由

defaultrouter="0.0.0.0"     # rc.conf项
route add default 0.0.0.0   #shell命令

#   建立路由

gateway_enable="YES"

#   添加路由

#2.0添加到1.0
route add -net 192.168.2.0/24 192.168.1.0     #shell命令
static_routes="n1"
route_n1="-net 192.168.2.0/24 192.168.1.0"    #rc.conf

#   网桥

ifconfig bridge create  #shell创建
ifconfig bridge destroy #shell销毁
fconfig bridge0
bridge0: flags=8802<BROADCAST,SIMPLEX,MULTICAST> metric 0 mtu 1500
        ether 96:3d:4b:f1:79:7a
        id 00:00:00:00:00:00 priority 32768 hellotime 2 fwddelay 15
        maxage 20 holdcnt 6 proto rstp maxaddr 100 timeout 1200
        root id 00:00:00:00:00:00 priority 0 ifcost 0 port 0
# 添加成员
ifconfig bridge0 addm fxp0 addm fxp1 up
ifconfig fxp0 up
ifconfig fxp1 up
#rc.conf
cloned_interfaces="bridge0"
ifconfig_bridge0="addm fxp0 addm fxp1 up"
ifconfig_fxp0="up"
ifconfig_fxp1="up"
#设置IP地址
ifconfig bridge0 inet 192.168.0.1/24
#生成树协议
ifconfig bridge0 stp fxp0 stp fxp1

#   链路聚合与故障转移

##   故障转移模式

ifconfig fxp0 up
ifconfig fxp1 up
ifconfig lagg0 create
ifconfig lagg0 up laggproto failover laggport fxp0 laggport fxp1 10.0.0.15/24
ifconfig_fxp0="up"
ifconfig_fxp1="up"
cloned_interfaces="lagg0"
ifconfig_lagg0="laggproto failover laggport fxp0 laggport fxp1 10.0.0.15/24"

##   IPNAT

sysrc natd_enable="YES" #开机启动
natd_interface="fxp0"   #网关网卡
natd_flags=""           #配置文件
#natd_flags="-f /etc/natd.conf"
vim /etc/natd.conf
redirect_port tcp 192.168.0.2:6667 6667
redirect_port tcp 192.168.0.3:80 80
#shell
natd -redirect_port proto targetIP:targetPORT[-targetPORT]
natd -redirect_port 协议(TCP UDP) 内部IP:端口  外部端口
或者 ipnat

本文链接：https://www.moebsd.cn/post/FreeBSD-networking.html
