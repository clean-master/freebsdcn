---
title: FreeBSD 换源方法
date: 2021-03-23 14:15:04
tags:
---

#   pkg 源:pkg源提供二进制安装包

FreeBSD 中pkg 源分为系统级和用户级两个源.不建议直接修改/etc/pkg/FreeBSD.conf,因为该文件会随着基本系统的更新而发生改变.

## 创建用户级源目录:

#mkdir -p /usr/local/etc/pkg/repos

## 创建用户级源文件:

#ee /usr/local/etc/pkg/repos/bjtu.conf
写入以下内容:

bjtu: {
  url: "pkg+http://freebsd-pkg.mirror.bjtulug.org/${ABI}/quarterly",
  mirror_type: "srv",
  signature_type: "none",
  fingerprints: "/usr/share/keys/pkg",
  enabled: yes
}
 FreeBSD: { enabled: no }
 
若要获取滚动更新的包,请将quarterly 修改为latest.请注意,CURRENT 版本只有latest.
若要使用https,请先安装security/ca_root_nss,并将http 修改为https,最后使用命令#pkg update -f 刷新缓存即可.
### 如果不能用，可以将域名freebsd-pkg.mirror.bjtulug.org 改为pkg.freebsd.cn 或 mirrors.ustc.edu.cn/freebsd-pkg 或 https://mirrors.163.com/freebsd-pkg/

#  ports源:提供源码方式安装软件的包管理器

创建或修改文件#ee /etc/make.conf:

写入以下内容:

MASTER_SITE_OVERRIDE?=http://freebsd-pkg.mirror.bjtulug.org/ports-distfiles/

## 如果不能用，可以将域名freebsd-pkg.mirror.bjtulug.org 更改为 https://mirrors.163.com/freebsd-ports/ 或 http://ports.freebsd.cn/

#  portsnap源:打包的ports文件

编辑portsnap 配置文件 #ee /etc/portsnap.conf :

将 SERVERNAME=portsnap.FreeBSD.org 修改为 SERVERNAME=freebsd-portsnap.mirror.bjtulug.org

获取portsnap 更新:

#portsnap fetch extract

## 如果不能用，可以将域名freebsd-portsnap.mirror.bjtulug.org 改为 portsnap.freebsd.cn

#  freebsd-update源:提供基本系统更新

编辑#ee /etc/freebsd-update.conf 文件:

将 ServerName update.FreeBSD.org 修改为 ServerName freebsd-update.mirror.bjtulug.org

## 如果不能用，可以将域名 freebsd-update.mirror.bjtulug.org 改为 update.freebsd.cn
## 例:从FreeBSD 12 升级到13.0

#freebsd-update -r 13.0-RELEASE upgrade
