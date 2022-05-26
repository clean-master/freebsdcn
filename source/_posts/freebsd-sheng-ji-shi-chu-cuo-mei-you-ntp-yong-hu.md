---
title: FreeBSD 升级时出错，没有ntp 用户
date: 2021-03-16 20:39:46
tags:
---

FreeBSD 升级出错，没有ntp 用户
终端执行命令

pw groupadd ntpd -g 123
pw useradd ntpd -u 123 -g ntpd -h - -d /var/db/ntp -s /usr/sbin/nologin -c "NTP Daemon"
本文链接：https://www.moebsd.cn/post/freebsd-update-no-ntp.html
