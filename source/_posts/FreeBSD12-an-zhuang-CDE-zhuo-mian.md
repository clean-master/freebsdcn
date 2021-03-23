---
title: FreeBSD12 安装CDE 桌面
date: 2021-03-23 14:06:39
tags:
---

#   配置环境
OS: FreeBSD 12.0-RELEASE amd64
Shell: csh tcsh 6.20.00
CPU: Intel i5-7200U (1) @ 2.712GHz
Memory: 145MiB / 217MiB
Vmware workstation Pro 15

#   开始安装
pkg install -y iconv bdftopcf libXScrnSaver ksh93 open-motif tcl86 xorg-fonts xorg-fonts-100dpi cde-2.3.1_1

##   安装完成cde后有提示怎样开启各项服务

sysrc rpcbind_enable=yes
sysrc dtspc_enable=yes
sysrc dtcms_enable=yes
service rpcbind start && service dtspc start && service dtcms start
ln -s /usr/local/dt/bin/Xsession ~/.Xsession
env LANG=C startx #这条命令执行失败时可以忽略

安装完成。

