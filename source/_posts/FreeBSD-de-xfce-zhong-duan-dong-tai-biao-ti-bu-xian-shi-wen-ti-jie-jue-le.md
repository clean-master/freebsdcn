---
title: FreeBSD 的xfce 终端动态标题不显示问题解决了：
date: 2021-03-16 20:04:23
tags:
---

tcsh 配置，home 目录创建.tcshrc,

写入以下配置

alias h history 25 alias j jobs -l alias la ls -aF alias lf ls -FA alias ll ls -lAF setenv EDITOR vi setenv PAGER less switch ($TERM) case "xterm*": set prompt="%{\033]0;[]%~\007%}%#" set filec set history = 1000 set savehist = (1000 merge) set autolist = ambiguous # Use history to aid expansion set autoexpand set autorehash breaksw default: set prompt="%#" breaksw endsw
