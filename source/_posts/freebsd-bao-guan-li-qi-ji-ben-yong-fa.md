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
----------------------------------------------------
如何使用多线程下载：
#pkg install axel #下载多线程下载工具#
新建或者编辑/etc/make.conf文件，写入以下两行：
FETCH_CMD=axel
FETCH_BEFORE_ARGS= -n 10 -a
FETCH_AFTER_ARGS=
DISABLE_SIZE=yes
------------------------------------------------
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

linux如gentoo上一般是直接 -jx 或者-jx+1 x为核心数。
FreeBSD ports 多线程编译
FORCE_MAKE_JOBS=yes
MAKE_JOBS_NUMBER=4
写入/etc/make.conf
没有就新建。4是处理器核心数，不知道就别改。 
#其他见 /usr/ports/Mk/bsd.port.mk

#   FreeBSD 如何安装软件

1：概括
FreeBSD捆绑了丰富的系统工具集合作为基础系统的一部分。此外，FreeBSD提供了两种用于安装第三方软件的补充技术：FreeBSD Ports Collection，用于从源代码安装，以及用于从预构建的二进制文件安装的软件包。这两种方法都可用于从本地媒体或网络安装软件。
2：了解
二进制包和端口之间的区别。

如何查找已移植到FreeBSD的第三方软件。

如何使用pkg管理二进制包。

如何使用Ports Collection从源代码构建第三方软件。

如何查找随应用程序一起安装的文件以进行安装后配置。

如果软件安装失败怎么办。
二进制包存储库中搜索应用
#pkg search subversion
使用Ports Collection的内置搜索机制
#cd /usr/ports # make search name=

提示：内置搜索机制使用索引信息文件。如果消息指示INDEX需要，则运行make fetchindex以下载当前索引文件。有了INDEX现在，make search将能够执行所请求的搜索。
pkg 教程
系统安装好后，是没有pkg这个软件的，但你可以直接使用，执行命令后，会有一个pkg脚本响应，并下载真正的pkg，下载安装后就，并把pkg链接到真正的pkg上，并把你的命令传递给真正的pkg，如果按照失败可以从ports编译安装
pkg info 查看已安装的软件包
pkg info pkg 查看pkg的版本
pkg install 安装软件
pkg del 删除软件
pkg upgrade 升级软件
pkg audit -F 审核软件
pkg autoremove 自动删除不需要的软件包
查找死包 pkg prime-list
作为依赖自动安装包，为自动程序包(活包）
（英语直译为自动包，中文简体，还没有这些内容，内容不知道几百年前的，台湾翻译没有写这些东西，根据自动删除那个，翻译为依包,依赖包简称？？？,我称为活包）
非依赖包我称为死包
#pkg set -A 1 devel/cmake
设为活包，将会加入自动删除列表
#pkg set -A 0 devel/cmake
设为死包 devel/cmake是指包名
#pkg clean 清楚过时或失效包
参数 -a 清楚包缓存
Ports Collection使用说明
如果没有安装，使用以下方法
portsnap fetch 获取
portsnap extract 提取/解压
portsnap fetch update更新

Ports Collection说明
Makefile：包含指定应如何编译应用程序以及应在何处安装组件的语句。

distinfo：包含必须下载以构建ports的文件的名称和校验和。

files/：这个目录包含程序在FreeBSD上编译和安装所需的任何补丁。此目录还可能包含用于构建ports的其他文件。

pkg-descr：提供程序的更详细说明。

pkg-plist：端口将安装的所有文件的列表。它还告诉ports系统在卸载时要删除哪些文件。
使用使用Portmaster升级ports
#cd /usr/ports/ports-mgmt/portmaster
#make install clean 安装
-a升级 -af升级并重建
