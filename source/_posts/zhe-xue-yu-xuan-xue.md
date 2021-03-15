---
title: FreeBSD 入门 哲学与玄学
date: 2021-03-16 03:00:04
tags:
---
# 『哲学与玄学』
FreeBSD 是一种 UNIX 哲学(如模块化，一切皆文件等，见《 UNIX 编程艺术》❩的发展，也是学院派的代表作品。她是一套工具集，她存在目的是为了让人们更好的生活。
# 『硬件支持』
截至 2020 年 12 月 22 日，FreeBSD 已经支持 intel 十代处理器显卡（ FreeBSD 12.2-STABLE / FreeBSD 13-CURRENT ），NVME PCI-E 硬盘，UEFI + GPT，Root 分区使用 ZFS 文件系统，部分树莓派等嵌入式设备，5G wifi，KDE Plasma 5，Clang + llvm 。
但是囿于硬件繁多，具体的设备支持还请看 https://www.freebsd.org/where.html 的 [ Hardware Compatibility List ] 部分。
有些网卡不支持可以购买 USB 网卡：推荐 COMFAST CF-WU810N 网卡。
显卡支持还请查看，总的来说对英特尔显卡支持比较好！
https://wiki.freebsd.org/Graphics
# 『软件安装』
包管理器。用过 Gentoo 的人可能对 FreeBSD 的 Ports 并不陌生， 因为 portage 正是脱胎于其中，见 [ https://wiki.gentoo.org/wiki/Project:Portage#About_Portage ”Portage is a GPLv2 package management system based on ports collections.”] 。
没有用过也不要紧，重新来过更具有挑战性。
FreeBSD 软件源共有四个，目前中国大陆境内尚无官方镜像站。(发邮件询问过但是并无详细的解释)
目前有多个非官方源可以正常使用：
网易 163 镜像站 [PKG+Ports]
freebsd.cn [ports pkg update portsnap 都有]
北京交通大学开源镜像站[理论上四类源都有，但 ports update 测试不可用，telegram 联系群组：bjtumirror]
USTC 开源镜像站[pkg+update]
要想成为一级官方镜像站，需要子域名 cn.freebsd.org ，但是境内 org 不能备案，也就不能开放 web 端口。这目前似乎是个无解的问题？
# 『学习资源』
相关书籍：《 Absolute FreeBSD 3rd 》。旧的变化也不是很大。不像 linux 有这么多入门书籍，什么 XX 秒精通 Linux，Linux XX 学，*linux* 。当然上边这些书，学 Linux 的也尽量别看，质量太差。但是由于历史上的原因，看 UNIX 相关书籍即可。
# 『捐赠事宜』
FreeBSD 官方基金会 https://www.freebsdfoundation.org/
最低限度 $10，支持 VISA 信用卡。有力者可捐赠一二。
