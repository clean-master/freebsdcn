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

本文链接：https://www.moebsd.cn/post/freebsd-install-xfce.html 
