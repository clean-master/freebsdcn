---
title: FreeBSD 安装xfce4
date: 2021-03-23 13:48:11
tags:
---

#   安装xorg

可选包 xorg 完整xorg环境包 xorg-minimal xorg最小化包

通过ports安装
cd /usr/ports/x11/xorg
make install clean

通过pkg安装
pkg install xorg

#   启动服务

syrc hald_enable="YES"
syrc dbus_enable="YES"
service hald start 
service dbus start

#   安装xfce4

通过ports安装
cd /usr/ports/x11-wm/xfce4
make install clean

通过pkg安装
pkg install xfce4

#   启用xfce

echo ". /usr/local/etc/xdg/xfce4/xinitrc" > ~/.xinitrc
或者
echo ". /usr/local/etc/xdg/xfce4/xinitrc" > ~/.xsession
根据条件使用

#   设置中文显示
在.xinitrc添加以下内容（但要在最前面才正常启用）
export LANG=zh_CN.UTF-8

#   可选配置

pkg install zh-fcitx(安装中文输入法，需要设置中文输入环境)
cd ~
ee .xinitrc文件添加以下内容
export XMODIFIERS="@im=fcitx"
export XIM_PROGRAM="fcitx"
export GTK_IM_MODULE="fcitx"
fcitx &


pkg install firefox（火狐浏览器）
pkg install smplayer (视频播放器)
pkg install zh_CN-libreoffice(办公软件)
pkg install gimp(图片处理)
pkg install thunderbird(邮件客户端)
pkg install wqy-fonts（安装文泉驿字体）
pkg install transmission (BT下载工具)

本文链接：https://www.moebsd.cn/post/freebsd-install-xfce.html
