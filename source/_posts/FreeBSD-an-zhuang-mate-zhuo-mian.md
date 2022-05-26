---
title: FreeBSD 安装mate 桌面
date: 2021-06-02 16:07:30
tags:
---

FreeBSD 安装mate 桌面环境

#   安装开始（主要程序）
pkg install -y mate-desktop mate xorg

在文件/etc/rc.conf 中加入下面的行
moused_enable="YES"
dbus_enable="YES"
hald_enable="YES"


#   安装 Slim 作为登陆管理器
pkg install -y slim

在/etc/rc.conf 中加入下面的行：

slim_enable="YES"

在主目录.xinitrc 文件加入下面的行。

echo exec mate-session >> .xinitrc

#   显示中文桌面环境
默认是csh，在.cshrc 中添加如下内容：
setenv LANG zh_CN.UTF-8
setenv LC_CTYPE zh_CN.UTF-8


#   安装输入法
pkg install zh-ibus-libpinyin（安装好运行初始化命令ibus-setup）
设置输入法变量
ee .xinitrc 
文件添加以下内容
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
ibus &


#   安装软件/安装字体
pkg install -y wqy-fonts
pkg install -y firefox
pkg install -y zh_CN-libreoffice

#   本文贡献者 QQ 雨天 2477294049
