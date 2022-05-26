---
title: 为FreeBSD 添加新字体
date: 2021-05-20 21:51:45
tags:
---

首先提取c:\windows\fonts 里所有的ttf 和ttc 字体文件。

为新字体新建一个目录便于管理：

mkdir -p /usr/local/share/fonts/WindowsFonts 

将字体文件复制进WindowsFonts 即可。

chmod -R +755 /usr/local/share/fonts/WindowsFonts 刷新权限，然后

sudo fc-cache 

即可.
