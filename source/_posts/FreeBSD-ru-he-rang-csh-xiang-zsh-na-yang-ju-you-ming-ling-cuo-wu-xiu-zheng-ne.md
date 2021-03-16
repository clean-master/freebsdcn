---
title: FreeBSD 如何让csh 像zsh 那样具有命令错误修正呢
date: 2021-03-16 00:50:20
tags:
---

比如你用 emacs写c ，但你输完emacs ma按tab回车是，他会匹配所有ma开头的文件，而这个是忽略掉，也就是按tab时不会在有你忽略的东西，对编程之类的友好，不用再匹配到二进制。.o之类的文件，

　　set correct = cmd lz/usr/bin tcsh>ls /usr/bin (y|n|e|a)?

　　set fignore = (.o \~) emacs ma[^D] main.c main.c~ main.o emacs ma[tab] emacs main.c
