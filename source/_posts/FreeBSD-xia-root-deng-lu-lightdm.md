---
title: FreeBSD 下root 登录 lightdm 
date: 2021-03-16 21:01:04
tags:
---

　　root 登录 lightdm freebsd下方法

　　pkg install lightdm-gtk-greeter lightdm

　　写入lightdm_enable=“YES”到rc.conf

　　编辑ee /usr/local/etc/lightdm/lightdm.conf

　　往下拉，找到greeter-show-manual-login=true 移除前面的#

　　编辑 ee /usr/local/etc/pam.d/lightdm

　　注释account requisite pam_securetty.so 这一行（往最前面加#）

　　service lightdm start 即可。
