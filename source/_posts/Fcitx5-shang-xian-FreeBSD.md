---
title: Fcitx5 上线 FreeBSD
date: 2021-03-16 00:50:20
tags:
---

　　Fcitx5 上线 FreeBSD


textproc/fcitx5
textproc/fcitx5-qt
textproc/fcitx5-gtk
textproc/fcitx5-configtool
chinese/fcitx5-rime
…

　　可通过 ports 安装。环境变量取决于你的窗口管理器和桌面以及 shell 。经测试不支持 slim，可能是配置问题。SDDM 可用。

　　自动启动：
cp /usr/local/share/applications/fcitx.desktop ~/.config/autostart/

　　在.cshrc 和 /etc/csh.cshrc 中进行如下配置，此配置可以解决部分窗口 fcitx 无效以及无法输入显示中文的问题。
setenv QT4_IM_MODULE fcitx
setenv GTK_IM_MODULE fcitx
setenv QT_IM_MODULE fcitx
setenv GTK2_IM_MODULE fcitx
setenv GTK3_IM_MODULE fcitx
setenv XMODIFIERS @im=fcitx
setenv LANG zh_CN.UTF-8
setenv MM_CHARSET zh_CN.UTF-8

　　在 root 用户下 rime 不会自动被添加到输入法，需要手动添加完成初始化！

　　SLIM 窗口下会提示IBUS 找不到……疑似bug。

我的博客即将同步至 OSCHINA 社区，这是我的 OSCHINA ID：FreeBSD中文社区，邀请大家一同入驻：https://www.oschina.net/sharing-plan/apply
