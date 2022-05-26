---
title: FreeBSD csh shell 配置
date: 2021-03-16 19:58:42
tags:
---

在/etc/csh.cshrc 里面加入：

alias ls ls –G, 并重新登录

问：如何让FreeBSD 的csh 像bash 那样按tab 列出列出无法补齐的候选文件？

答：标准的方法是按Ctrl+D。

但如果一定要用tab 的话，在/etc/csh.cshrc 中加入：set autolist ​​​​
