---
title: FreeBSD 安装KDE5 桌面
date: 2021-06-02 16:19:35
tags:
---

#   1.安装
pkg install -y xorg sddm kde5 wqy-fonts

#   2.配置
ee /etc/fstab
添加内容如下:

proc /proc procfs rw 0 0

ee /etc/rc.conf
添加：
dbus_enable="YES"
hald_enable="YES"
sddm_enable="YES"

echo "exec /usr/local/bin/startkde" > ~/.xinitrc

##   注意：SDDM root登陆
修改/usr/local/etc/pam.d/sddm文件把四处位于include之后的login替换成system（root登陆需要）


#   中文化
点击开始->System Settings->Regional Settings 在Language项的Available Language栏中找到“简体中文”单击“>”将其加到 Preferrred Languages栏中，然后单击Apply按钮；再到Formats项，将Region文本框中的内容修改为“中国-简体中文(zh-CN)，单击Apply按钮，logout（注销）后重新登录，此时系统语言将变为中文。

##   中文输入法安装
见其他教程。

#   本文贡献者 QQ 雨天 2477294049
 
