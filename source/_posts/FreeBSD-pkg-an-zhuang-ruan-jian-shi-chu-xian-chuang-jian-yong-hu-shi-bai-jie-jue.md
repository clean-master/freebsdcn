---
title: FreeBSD pkg 安装软件时出现创建用户失败解决
date: 2021-03-16 20:41:19
tags:
---

　　问题示例：

[1/1] Installing package...
===> Creating groups.
Creating group 'package' with gid '000'.
===> Creating users
Creating user 'package' with uid '000'.
pw: user 'package' disappeared during update
pkg: PRE-INSTALL script failed
　　问题解析：数据库未同步
　　问题解决:

/usr/sbin/pwd_mkdb -p /etc/master.passwd
