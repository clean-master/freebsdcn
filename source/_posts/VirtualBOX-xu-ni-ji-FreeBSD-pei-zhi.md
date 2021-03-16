---
title: VirtualBOX 虚拟机 FreeBSD配置
date: 2021-03-16 20:43:59
tags:
---

　pkg 装virtualbox-ose-additions，

　　再将


Section "Device"
Identifier "Card0"
Driver "vboxvideo"
VendorName "InnoTek Systemberatung GmbH"
BoardName "VirtualBox Graphics Adapter"
EndSection


　　写到/usr/local/etc/X11/ xorg.conf

　　显卡控制器用VBoxSVGA
