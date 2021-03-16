---
title: FreeBSD 13.0 已经发布 从现有版本更新到13
date: 2021-03-16 20:58:57
tags:
---

 #freebsd-update -r 13.0-RELEASE upgrade

如果提示更新第三方软件后，再执行freebsd-update install ，

请输入 #pkg update && pkg upgrade

然后输入 #freebsd-update install

提示重启 #reboot #freebsd-update install 即可，

查看版本 #freebsd-version 完毕。

此外，update源可以用 update.FreeBSD.cn
