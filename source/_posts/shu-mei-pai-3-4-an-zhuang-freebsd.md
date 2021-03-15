---

title: 树莓派3/4 安装 FreeBSD

date: 2021-03-16 05:57:23

tags:

---

已盼春来归 已盼春来归 今日去 愿为春来归 盼归

春天来了 FreeBSD 的春天在哪里?

　　树莓派是什么，相信凡是关注了我们的人都不会不知道，但是介于非专业人员需要在此做简要介绍。我们的安卓手机，大部分的 ARM 芯片的，即使歌曲《华为美》所谓的“中国芯”也是来源于 ARM 的专利授权，没了授权，什么芯也不是。

　　而树莓派就是一块使用 ARM 芯片的开发板，就是一块接口丰富（ HDMI 、I2C 、USB X 4 、POE 模块等等）的电路板，相当于配置较低的手机，手机能做的事情，树莓派都能做。一般用于嵌入式开发，比如机器人，路由器和监控等等。

　　 FreeBSD 对架构的支持是按照等级划分的，ARM 属于二级架构，所以软件支持上不如 AMD64，一些软件无法通过 ports 以源码的形式进行编译，比如编译 X11/xorg 就会遇到很多错误（已经报告 bug 列表）。

　　树莓派 3B+是目前配置比较高的型号，由于 FreeBSD 的 SDIO 驱动并未完全支持，所以板载的蓝牙和 WIFI 均无法使用（可购买无线网卡，推荐 16 块钱的 COMFAST CF-WU810N ）。

　　自树莓派 3B+开始，无需任何改动，系统即可从 U 盘启动，我测试了 FreeBSD12/13 都是支持的，但是速度非常慢，一方面树莓派使用 USB2.0 极大的限制的总线速度，另一方面可能是玄学问题。（我人丑？我用的是东芝（ TOSHIBA ） 64GB USB3.0 U 盘 U364 高速迷你车载 U 盘）.

　　因此不建议使用 U 盘启动，慢的我要打年年猫，年年猫是谁？是一只调皮的狸花猫而已。

　　我们所有要准备的有树莓派 3B+板子一块，网线一段，存储卡一枚。从华为云镜像站（速度较快）下载适用于树莓派 3B+的镜像，12 和 13 我用起来感觉都一样，不过 13 的 LLVM 版本太新，很多软件编译不过去，所以还是用 12 的吧。

https://mirrors.huaweicloud.com/freebsd/snapshots/ISO-IMAGES/13.0/FreeBSD-13.0-CURRENT-arm64-aarch64-RPI3-20200116-r356767.img.xz 　（该链接不是固定的找不到就去 https://mirrors.huaweicloud.com/freebsd/snapshots/ISO-IMAGES/13.0 ）

　　下载后解压缩。使用 rufus 刻录。插入网线，将存储卡插入树莓派，通电等待约五分钟，查看路由器后台获取 IP 。

　　使用 XShell 即可登录树莓派。用户名密码均为 freebsd 。root 需要登录后输入 su，密码为 root 。可通过更改

　　/etc/ssh/sshd_config

　　文件来开启 root 账户的 ssh 远程登录权限。

　　方法：

　　编辑 /etc/sh/sshd_config （注意是 sshd 不是 ssh ！这是两个文件），修改或者加入

　　PermitRootLogin yes #允许 root 登录

　　PasswordAuthentication yes # 设置是否使用口令验证。

　　（也可以把对应行前面的注释#去掉，注意 PermitRootLogin 一行默认是 no，去掉后要改成 yes 。即 PermitRootLogin yes ）。

　　然后重启服务：

　　server sshd restart

　　然后就是时间设置问题，树莓派没有板载的纽扣电池确保 CMOS 时钟准确。所以完全依靠 NTP 服务来校正时间，如果时间不准确，将影响很多服务的运行，比如无法执行 portsnap fetch 命令。

　　方法很简单：

　　在 /etc/rc.conf 中加入

　　ntpd_enable="YES"

　　ntpdate_enable="YES"

　　ntpdate_program="ntpdate"

　　ntpdate_flags="0.cn.pool.ntp.org"

　　然后开启时间服务器：

　　server ntpdate start

　　输入 date 查看时间，完成校时。我国使用 UTC+8 北京时，虽然不更改不会影响软件使用，但看起来不方便，可通过 bsdconfig 命令将地区调整到亚洲 /中国 /上海。

　　树莓派应该会自动接通互联网，所以不必考虑联网问题。

　　如果你购买了上述无线网卡，想实现开机自动连接 wifi 的功能，那也非常简单。

　　方法：

　　/boot/loader.conf

　　中写入

　　rtwn_usb_load="YES"

　　legal.realtek.license_ack=1

　　在 /etc/rc.conf 中写入

　　wlans_rtwn0="wlan0"

　　ifconfig_wlan0="WPA DHCP"

　　注意在 /etc/wpa_supplicant.conf 文件中（没有就自己通 touch 命令新建一个）写入

　　network={ ssid="wifi 名字，别搞什么中文" psk="密码" }

　　保存重启即可。能够实现开机自动连接 wifi 。

　　安装 GUI 更简单，pkg install xorg mate 即可。可使用 VNC 或者 XRDP 服务。都很简单不再赘述。

　　默认 HDMI 是可以直接输出的无需调整，对于一般 linux 所使用的参数，freebsd 也同样支持，比如超频。文件位置，改动也相同，不再赘述。

　　总的来说树莓派 3B+的配置还是太差了，尤其是处理器和 USB2.0 以及内存方面，期待树莓派 4 以及 FreeBSD SDIO 驱动的早日出现。慈悲！

　　雁南飞这首歌使我想起了小学的一篇课文《燕子专列》：瑞士有一年由于气温骤降大雁来不及南飞，人们在号召下使用列车将燕子送往温暖故乡的故事。吾乡何处呢？

　　我闻到点燃木头的味道总是想起一些事情，究竟是什么我不知道，只是痕迹越来越淡了。

　　对于树莓派 3b+/4 来说，目前除了没有 WIFI，其余均正常使用。

　　QQ 交流群 817507910
