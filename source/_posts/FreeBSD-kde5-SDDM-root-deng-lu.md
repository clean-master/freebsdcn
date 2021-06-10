---
title: FreeBSD KDE5 SDDM root登录
date: 2021-06-10 22:52:16
tags:
---


更改/usr/local/etc/pam.d/sddm文件
把include之后的login，替换成system，一共4个。
之后就可以以root登录sddm了！

###   注意sddm 左下角选项不能为Wayland ，应该是Plasma-X11，选错无法登陆！
