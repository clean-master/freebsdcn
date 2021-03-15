---
title: FreeBSD 包管理器基本用法
date: 2021-03-16 05:35:54
tags:
---
#   FreeBSD 包管理器设计理念

熟悉 Linux 的人也许会发现，FreeBSD 的包管理方案实际上大约等于以下两大 Linux 发行版包管理器的完美合体：

Arch: pacman，对应 pkg（秉承同样的 KISS 理念）

Gentoo: Portage，对应 Ports（Portage 本身就是 Ports 的仿制品）

#   FreeBSD pkg基础教程1

装上系统默认没有pkg，先获取pkg：
#pkg 回车即可输入y 确认下载
————————————————————————————————————
pkg使用https，先安装ssl 证书：
#pkg install ca_root_nss
然后把repo.conf 里的pkg+http 改成pkg+https 即可。
最后刷新pkg数据库：pkg update -f
————————————————————————————————————
安装python 3：
#pkg install python
————————————————————————————————————
pkg 升级：
#pkg upgrade
———————————————————————————————————-—
错误：You must upgrade the ports-mgmt/pkg port first
解决：
#cd /usr/ports/ports-mgmt/pkg
#make deinstall reinstall

#   FreeBSD ports 基本用法

首先获取portsnap
#portsnap fetch extract
---------------------------------------
使用whereis 查询软件地址
如#whereis python 回应：
#whereis python
输出 
python: /usr/ports/lang/python
--------------------------------------------
如何安装python3：
#cd /usr/ports/lang/python
#make BATCH=yes clean
其中BATCH=yes 的意思是使用默认配置
------------------------------------------------------
如何使用多核心编译？

linux如gentoo上一般是直接 -jx 或者-jx+1 x为核心数。
新建或者编辑/etc/make.conf文件，写入以下两行：
FORCE_MAKE_JOBS=yes
MAKE_JOBS_NUMBER=4
#其他见 /usr/ports/Mk/bsd.port.mk
----------------------------------------------------
如何使用多线程下载：
#pkg install axel #下载多线程下载工具#
新建或者编辑/etc/make.conf文件，写入以下两行：
FETCH_CMD=axel
FETCH_BEFORE_ARGS= -n 10 -a
FETCH_AFTER_ARGS=
DISABLE_SIZE=yes
进阶：如果不选择BATCH=yes 的方法手动配置依赖：
看看python 的ports 在哪：
#whereis python
python: /usr/ports/lang/pytho
安装python3：
#cd /usr/ports/lang/python
如何设置全部所需的依赖：
#make config-recursive
如何一次性下载所有需要的软件包：
#make BATCH=yes fetch-recursive

三.升级 ports collection

1 portsnap fetch extract
四.FreeBSD 包升级管理工具
首先更新Ports树
portsnap fetch update
然后列出过时Ports组件
pkg_version -l '<'
下边分别列出2种FreeBSD手册中提及的升级工具:
一、portupgrade
cd /usr/ports/ports-mgmt/portupgrade &&make install clean
portupgrade -ai #自动升级所有软件
portupgrade -R screen #升级单个软件

二、portmaster （推荐）

cd /usr/ports/ports-mgmt/portmaster && make install clean
portmaster -ai #自动升级所有软件
portmaster screen#升级单个软件
portmaster -a -m "BATCH=yes" 或者-D -G --no-confirm 都可以免除确认

#    FreeBSD ports 多线程编译

FreeBSD ports 多线程编译
FORCE_MAKE_JOBS=yes
MAKE_JOBS_NUMBER=4
写入/etc/make.conf
没有就新建。4是处理器核心数，不知道就别改。 
