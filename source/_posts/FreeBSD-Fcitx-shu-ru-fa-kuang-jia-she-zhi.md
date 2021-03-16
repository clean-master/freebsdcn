---
title: FreeBSD Fcitx 输入法框架设置
date: 2021-03-16 00:50:20
tags:
---

在.cshrc 和/etc/csh.cshrc 中进行如下配置，此配置可以解决部分窗口fcitx 无效的问题。

setenv QT4_IM_MODULE fcitx

setenv GTK_IM_MODULE fcitx

setenv QT_IM_MODULE fcitx

setenv GTK2_IM_MODULE fcitx

setenv GTK3_IM_MODULE fcitx

setenv XMODIFIERS @im=fcitx


在.cshrc 和/etc/csh.cshrc 中进行下面两行配置可以解决终端无法输入中文和无法显示中文的问题。

setenv LANG zh_CN.UTF-8

setenv MM_CHARSET zh_CN.UTF-8


接Fcitx 输入法补充：

要想终端不乱码还需要

setenv LANG zh_CN.UTF-8

setenv LC_CTYPE zh_CN.UTF-8

setenv LC_ALL zh_CN.UTF-8 
