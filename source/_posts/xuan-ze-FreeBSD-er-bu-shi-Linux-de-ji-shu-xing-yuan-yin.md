---
title: 选择 FreeBSD 而不是 Linux 的技术性原因
date: 2021-03-16 20:52:31
tags:
---

干净的分离
在 FreeBSD 的设计方式下，不同的组件组合在一起的，处理配置和调优，以及多年来开发和改进的所有工具，使得使用 FreeBSD 是一件很特别的事情。
从 1998 年开始，我所使用的大多数 GNU/Linux 发行版，你都会有一种 "不匹配 "的感觉。
举个例子，Debian GNU/Linux 有 Debian 的做事方式。Debian 的方式是通过使用一套特定的配置管理工具和补丁来使第三方软件符合 "Debian 方式 "的设置。虽然这在某种意义上可以统一你在 Debian 发行版上的做事方式，但它却打破了上游的配置，这让人非常烦恼。特别是当某些东西不正常，或者上游文档中描述的方式与 Debian 上的设置不一致时，这个问题就更严重了。这种方法的另一个问题是，一些第三方软件，甚至是发行版的核心元素，比如 systemd，都不能强行按照 "Debian 的方式 "去做。其结果是，系统的某些部分以 "Debian 方式 "运行，而其他部分则不是。Debian GNU/Linux 采用了 systemd，但同时默认的网络部分是 Debian 特有的。有时你必须禁用或移除 Debian 特定的东西才能让 systemd 特定的东西工作。
在像 Arch Linux 这样的发行版上，这个问题是不存在的，因为不存在 "Arch 方式 "这样的东西。Arch Linux 发行版希望第三方软件能够像上游一样，所以除非绝对必要，否则他们不会改变任何东西。这很好，因为这意味着上游文档与软件相匹配。然而，这种方法的一个问题是，由于第三方软件确实以不同的方式处理事情，你可能最终会得到一个软件运行不统一的系统。然而，在系统管理方面，我个人还是更喜欢 Arch Linux，而不是 Debian，因为 Debian 有时几乎会修改全部的第三方软件。
Ubuntu 就更糟糕了。因为它是基于 Debian 的，所以运行时使用了很多 Debian 的工具和设置，但同时也有 "Ubuntu 方式"，即在 Debian 的基础上改变了一些东西，然后在这些基础上又增加了一层，即所谓的用户改进工具层，这有时会使 Ubuntu 出现难以理解的故障——即内部错误。
在 FreeBSD 上，你会马上发现，你所面对的是一个非常完善的系统。
内核和基本系统与第三方应用程序是完全分离的，基本系统的配置进入 /etc，而所有第三方的配置进入 /usr/local/etc 。所有你可以配置的东西，所有你可以调整或设置的东西都在 man 手册中有很好的记录。
你所有的东西，从 rc 实用程序（也就是被 init 调用后控制自动启动过程的命令脚本）到命令脚本，再到 sysctl 内核管理工具，所有不同的系统配置，以及其他所有的东西都放在一起，而且存储的很好。
我不知道该如何准确地表达这一点，但因为 FreeBSD 的管理方式，是作为一个完整的操作系统和项目来管理的，而不是作为一堆不同的项目被粘合在一个发行版中，所以一切都考虑得非常周全。它是基于多年经验上的，当事情发生变化时，它们会为了整个社区的利益而变化，并且有很多来自真实使用案例和行业问题的反馈。
要真正理解这一点，最好的方法之一是阅读 Michael W. Lucas 的《 Absolute FreeBSD 》一书。他不仅解释和描述了书中涉及的所有技术问题，而且还抓住了重要的历史背景来解释为什么事情会是这样的。

文档
有些人不认为文档是采用某项技术 /工具原因的一部分，但文档属于它所描述的技术的集成部分。糟糕的、过时的和缺失的文档应该被认为是一个 Bug 。
FreeBSD 的文档是随系统附带的，所以你不必在网上搜索。基本系统的 handbook 手册质量很好，而且是专门为 FreeBSD 编写的。您所需要的大部分内容都在系统中。
FreeBSD 也有 FreeBSD 手册，它涵盖了 FreeBSD 的安装和日常使用所需。FreeBSD 手册可以在安装过程中本地安装。这本手册偶尔会有一些过时的部分，因为这本书是许多人持续工作的结果，但它一般都会更新，而且写得很好。

安全
通常情况下，被入侵的不是操作系统，而是运行在操作系统上的程序。在某些情况下，被入侵的程序可以与操作系统进行交互，从而也会影响到操作系统。保护操作系统的安全意味着您要确保计算机的资源只被授权的人用于授权的目的。
FreeBSD 经过了彻底的审计，以消除缓冲区溢出和其他无数的安全问题，此外，FreeBSD 还提供了许多工具和选项来帮助您保护系统免受攻击。
我不可能在这篇文章中提供一份详尽的选项和可用功能的清单，因为 FreeBSD 的安全主题可以轻松地写满一本书。如果您想更深入地了解 FreeBSD 的一些安全特性，我强烈推荐 Michael W. Lucas 的《 Absolute FreeBSD 》一书。
不过，我还是要提几件事情。

在安装 FreeBSD 的过程中，安装程序提供了一系列可以启用或禁用的选项。

隐藏其他 UID 进程
隐藏其他 GID 进程
隐匿已被囚禁的进程
隐藏信息缓冲区
禁用进程调试
随机化进程 ID
禁用 syslogd 网络
禁用 Sendmail
安全控制台
非可执行堆栈和堆栈保护
大多数 FreeBSD 的内核级安全设置都可以在 security.bsd sysctl 树中找到，而且每隔几个月就会有更多的设置被添加进来。您可以运行 sysctl -d security.bsd 来显示您的 FreeBSD 安装中的可用选项。
#sysctl -d security.bsd
security.bsd: BSD security policy
security.bsd.stack_guard_page: Specifies the number of guard pages for a stack that grows
security.bsd.unprivileged_get_quota: Unprivileged processes may retrieve quotas for other uids and gids
security.bsd.hardlink_check_gid: Unprivileged processes cannot create hard links to files owned by other groups
security.bsd.hardlink_check_uid: Unprivileged processes cannot create hard links to files owned by other users
security.bsd.unprivileged_idprio: Allow non-root users to set an idle priority
security.bsd.unprivileged_proc_debug: Unprivileged processes may use process debugging facilities
security.bsd.conservative_signals: Unprivileged processes prevented from sending certain signals to processes whose credentials have changed
security.bsd.see_jail_proc: Unprivileged processes may see subjects/objects with different jail ids
security.bsd.see_other_gids: Unprivileged processes may see subjects/objects with different real gid
security.bsd.see_other_uids: Unprivileged processes may see subjects/objects with different real uid
security.bsd.unprivileged_read_msgbuf: Unprivileged processes may read the kernel message buffer
security.bsd.unprivileged_mlock: Allow non-root users to call mlock(2)
security.bsd.suser_enabled: processes with uid 0 have privilege
security.bsd.map_at_zero: Permit processes to map an object at virtual address 0.

漏洞统计
这是一个 FreeBSD 和 Linux 的漏洞统计列表。FreeBSD 上的安全问题数量普遍较少，这并不一定意味着 FreeBSD 比 Linux 更安全，尽管我相信是这样，但也可能是因为 Linux 上有更多的用户。
+---------+---------+-------+
| Year | FreeBSD | Linux |
+---------|---------|-------+
| 1999 | 18 | 19 |
| 2000 | 27 | 5 |
| 2001 | 36 | 22 |
| 2002 | 31 | 15 |
| 2003 | 14 | 19 |
| 2004 | 15 | 51 |
| 2005 | 17 | 133 |
| 2006 | 27 | 90 |
| 2007 | 9 | 62 |
| 2008 | 15 | 71 |
| 2009 | 11 | 102 |
| 2010 | 8 | 123 |
| 2011 | 10 | 83 |
| 2012 | 10 | 115 |
| 2013 | 13 | 189 |
| 2014 | 18 | 130 |
| 2015 | 6 | 86 |
| 2016 | 6 | 217 |
| 2017 | 23 | 454 |
| 2018 | 29 | 177 |
| 2019 | 18 | 170 |
|---------|---------|-------|
| Total | 361 | 2333 |
+---------+---------+-------+
有关特定漏洞的进一步信息，您可以查看 FreeBSD 和 Linux 的 CVE 详情网站。

稳定性
FreeBSD 有很好的工程和发布管理经验。FreeBSD 从构思到公开发布要经过多个步骤。
当有人有了一个想法，并开发了一些新的东西，它首先会得到同行审查。然后它进入 "CURRENT"分支进行综合测试，并根据复杂程度或潜在影响，调整进入稳定版的迁移窗口。然后它进入 "STABLE"分支进行更广泛的用户群测试。这通常是所有测试版测试发生的地方，也有更广泛的社区参与。然后，它进入发布候选版本测试，通常持续 3 轮，然后成为一个正常的版本。
这意味着只要你了解发布和升级的注意事项，你就可以很有信心相信系统正常运行。
软件的补丁发布是为了修复任何漏洞和错误。
这通常使 FreeBSD 成为一个非常可靠的操作系统。

Ports
FreeBSD Ports 是一个惊人的工程壮举。NetBSD 的 pkgsrc (package source) 和 OpenBSD 的 ports collection 都源于 FreeBSD ports 系统。
通常当您在 Unix 操作系统上安装软件时，您需要找到并下载软件。然后解压软件，通常是压缩的 tar 包。然后在 INSTALL 、README 等其他文本文档中找到文档， 并阅读关于如何安装软件的说明。如果软件是以源码格式发布的，你需要编译它，这通常涉及到编辑一个 Makefile 或运行一个 configure 脚本。如果编译成功，你就需要测试和安装软件。如果软件有依赖性， 则需要先下载并安装这些依赖性。
FreeBSD ports Collection 使用 Makefile 来自动完成编译、 安装和卸载软件的过程， 并使用 make 命令。组成 port 的文件包含了所有必要的信息， 以便自动下载、 解压缩、 打补丁、 编译和安装应用程序， 而在 ports 目录下发出诸如 make install 或 make install clean 这样的开始命令之后， 用户只需要很少的干预 (如果有的话)。如果 port 需要依赖其它应用程序或库， 则会事先自动安装。
大多数 port 都配置了一组默认的选项， 这些选项被认为是适合大多数用户的。然而， 这也是 ports 系统的一大优点， 这些配置选项可以在安装前使用 make config 命令进行修改。该命令会弹出一个基于文本的界面， 允许用户选择所需的选项。
在写这篇文章的时候，集合中有超过 38487 个端口可用
在大多数情况下，ports 应用程序都是以预编译包的形式提供下载的， 并设置了默认的选项。这些软件包可以通过 FreeBSD pkg - Binary Package Management 应用程序来安装。预先编译的 port 被称为 "package"。
FreeBSD 项目有一个软件包联编场， 其中联编了所有支持的架构和主要版本的软件包。数据库中提供了所有软件包的联编日志和已知错误， 而每周的联编日志也可以通过邮件列表存档获得。

滚动发行软件包
在软件包方面，您有两个不同的分支可以选择。一个叫 "quarterly"，另一个叫 "latest"。
Quarterly 是在每年 1 月、4 月、7 月和 10 月的季度开始时， 从修订系统中的 HEAD 分支中切割出来的 Ports 分支的名称， 也是由这些分支产生的二进制软件包集的名称。
Quarterly 分支为用户提供了更加可预测和稳定的 ports 和包的安装和升级体验。这基本上是通过只允许非功能更新来实现的。季度分支的目标是接收安全修复， 但也可能有版本更新， 或提交的回溯， 错误修复和 ports 合规性或框架变化。
如果您选择了 "latest"的分支，FreeBSD 就会成为第三方软件包的滚动发行版， 而且和 Arch Linux 很像， 它也会得到最新的软件。

Poudriere
Poudriere 是一个用于创建和测试 FreeBSD 软件包的工具。它利用 FreeBSD jail 系统来建立独立的编译环境。这些 jail 可以用来为不同版本的 FreeBSD 编译软件包。一旦这些软件包被编译完成，它们的布局就会与官方镜像相同。这些软件包可以被 FreeBSD pkg 二进制软件包管理工具所使用。
Poudriere 是一个用于测试和构建软件包的神奇工具，通过 Poudriere，您可以轻松地构建和设置自己的二进制软件包库，其中的软件包将完全按照您的规格和需求构建。
Poudriere 可以处理整个 ports 树的批量联编，ports 树的特定子集， 或包括其依赖关系在内的单个 port 。它能够自动地联编软件包， 生成联编日志文件， 提供一个经过签名的 pkg 仓库， 使得它能够在提交一个补丁到 FreeBSD bug 跟踪器之前测试 port 联编过程， 使得它能够使用不同的选项来测试不同的联编过程。Poudriere 在一个干净的 Jail 环境中进行联编， 在这个环境中， 它能够使用 zfs 的特定功能。这意味着没有对主机环境的污染，没有剩余的文件，没有意外的删除，没有对现有配置文件的修改。
Poudriere 的设置和使用非常简单，因为它没有任何依赖，并且可以在任何支持的 FreeBSD 版本上运行。

ZFS
ZFS 文件系统是 FreeBSD 上的一等公民。这不仅意味着可以在 ZFS 上安装根目录，安装程序也支持这一点，而且还意味着很多基础系统工具都已经紧密地集成或构建了对 ZFS 的支持。在 FreeBSD 上运行 ZFS 和在 Linux 上运行 ZFS 是不同的。在 FreeBSD 上，你会得到更多的工具，可以用来研究 ZFS 的性能问题或其他相关问题。
ZFS 的一些特点是（摘自维基百科）。
设计用于长期的数据存储，无限扩展的数据存储大小，零数据丢失，高配置性。
对所有数据和元数据进行分层校验和，确保整个存储系统在使用时可以进行验证，并确认是否正确存储，如果损坏则进行补救。校验和存储的是块的父块，而不是块本身。这与许多文件系统形成鲜明对比，在这些系统中，校验和（如果持有）与数据一起存储，因此，如果数据丢失或损坏，校验和也可能丢失或不正确。
可以存储用户指定数量的数据或元数据副本，或选定的数据类型，以提高重要文件和结构的数据损坏后的恢复能力。
在某些情况下，在发生错误或不一致的情况下，自动回滚最近对文件系统和数据的更改。
当检测到数据不一致和写入失败时，对于数据能够重建的所有错误，自动和（通常）无声地自愈。数据可以通过以下方式重建：存储在每个块的父块中的错误检测和校正校验和；磁盘上保存的多个数据副本（包括校验和）；在 SLOG （ ZIL ）上记录的应该发生但没有发生的写入意图（断电后）； RAID/RAIDZ 磁盘和卷的奇偶校验数据；镜像磁盘和卷的数据副本。
标准 RAID 级别和额外的 ZFS RAID 布局（"RAIDZ"）的本地处理。为了提高效率，RAIDZ 级别只在所需的磁盘上进行数据剥离（许多 RAID 系统在所有设备上不加区分地进行剥离），而校验和允许重建不一致或损坏的数据，以最小化有缺陷的块。
原生处理分层存储和缓存设备，这通常是一个与卷相关的任务。因为 ZFS 也了解文件系统，所以它可以利用文件相关的知识来告知、整合和优化其分层存储处理，这是单独的设备无法做到的。
对快照和备份 /复制的本地处理，可以通过整合卷和文件处理来提高效率。相关工具提供的水平较低，需要外部脚本和软件才能利用。
原生的数据压缩和重复数据删除，不过后者主要在 RAM 中处理，且对内存有一定的消耗。
高效重建 RAID 阵列--RAID 控制器经常需要重建整个磁盘，但 ZFS 可以结合磁盘和文件知识，将任何重建限制在实际丢失或损坏的数据上，大大加快了重建速度。
不受 RAID 硬件变化的影响，而这些变化会影响许多其他系统。在许多系统中，如果自带的 RAID 硬件（如 RAID 卡）发生故障，或者数据被移动到另一个 RAID 系统中，文件系统将缺少原 RAID 硬件上的信息，而这些信息是管理 RAID 阵列上的数据所需要的。这可能会导致数据的完全丢失，除非能够获得接近相同的硬件并作为 "垫脚石"。由于 ZFS 自己管理 RAID，所以 ZFS 池可以迁移到其他硬件上，或者重新安装操作系统，RAIDZ 结构和数据将再次被 ZFS 识别并立即访问。
能够识别出本来可以在缓存中找到但最近反而被丢弃的数据，这使得 ZFS 可以根据以后的使用情况重新评估其缓存决策，有利于实现非常高的缓存命中率（ ZFS 缓存命中率通常超过 80%）。
对于那些原本会造成数据处理延迟的数据，可以使用替代的缓存策略。例如，能够减慢存储系统速度的同步写入可以通过写入一个快速的独立缓存设备，即 SLOG （有时称为 ZIL--ZFS 意图日志）来转换为异步写入。
高度可调性--许多内部参数可以被配置为最佳功能。
可以用于高可用性集群和计算，尽管不是完全为这个用途设计的。
当然，当你在 Linux 上使用 ZFS 运行时，你也能获得所有这些功能。然而，这其中有一个很大的区别，因为没有任何一个 Linux 发行版甚至接近 FreeBSD 与 ZFS 的集成程度。

启动环境
由于与 ZFS 的紧密集成，FreeBSD 也支持引导环境。通过启动环境，您可以安装多个版本的核心操作系统，并选择其中的一个来启动。因此，启动环境是一个可启动的系统的克隆或快照。有了启动环境，你可以对系统进行防弹升级或更改，你不必担心破坏任何东西，因为你总是可以回滚。
这也意味着您可以在新的 ZFS 引导环境中更新 FreeBSD 系统，而无需接触正在运行的系统。您也可以在 FreeBSD Jail 中进行升级和测试结果。您甚至可以将 ZFS 引导环境复制或移动到另一台机器上。
FreeBSD 的 bectl 工具可以让您轻松管理启动环境。

BSD 启动
FreeBSD 使用传统的 BSD 风格的 init 。
在 BSD 风格的 init 中，没有运行级别，也不存在 /etc/inittab 。取而代之的是，启动是由 rc 脚本来控制的。
在 /etc/rc.d/中找到的脚本是为基本系统的应用程序服务的，比如 cron 、sshd 、syslog 等。而 /usr/local/etc/rc.d/中的脚本则是用户安装的第三方应用程序， 例如 NGINX 或 Postfix 。
如前所述， 由于 FreeBSD 是作为一个完整的操作系统而开发的， 用户安装的第三方应用程序并不是基本系统的一部分。第三方应用程序是通过包或端口来安装的。为了保持它们与基本系统的分离， 用户安装的应用程序被安装在 /usr/local/ 下。因此，用户安装的二进制文件位于 /usr/local/bin/，而配置文件则位于 /usr/local/etc/。
在 BSD 初始化系统中，通过在 /etc/rc.conf 中添加服务条目来启用服务。默认设置位于 /etc/defaults/rc.conf 中，这些默认设置会被 /etc/rc.conf 中的设置所覆盖。
下面的 /etc/rc.conf 中的条目可以启用 sshd 。

sshd_enable="YES"
你可以手动添加条目，也可以运行。

#service sshd enable
这将自动编辑 /etc/rc.conf 并添加条目。

你可以用以下方法手动启动一个服务： # service sshd start

#service sshd start
如果一个服务没有被启用，但你仍然想启动它，可以使用命令行启动它。

#service sshd onestart
你可以在维基百科上阅读更多关于 init 系统的内容。

jail
FreeBSD Jails 系统是另一个惊人的工程壮举。
在 2000 年 3 月 14 日的 4.0 版本中，FreeBSD 引入了 jails 系统。
FreeBSD jail 是一种操作系统级的虚拟化，它允许您将一个 FreeBSD 衍生的系统安装到多个独立的迷你系统中，称为 jails 。运行在 jail 中的系统共享相同的内核和系统资源，因此开销非常小。
对 FreeBSD jails 的需求来自于一个小型共享环境主机提供商 (R&D Associates, Inc.的所有者，Derrick T. Woolworth)的愿望，即在他们自己的服务和客户的服务之间建立一个干净、清晰的分离，主要是为了安全和便于管理。解决方案（由 Poul-Henning Kamp 开发）不是增加一层新的细粒度配置选项，而是对系统进行分门别类，包括其文件和资源，只有合适的人才能访问合适的分门别类。
通过 jail，可以创建各种虚拟机，每个虚拟机都有自己的一套实用程序和自己的配置。这使得它成为一种安全的试用软件的方式。例如，可以在不同的 jail 中运行不同版本或尝试不同配置的 web 服务器包。而且由于 jail 限定在一个狭小的范围内，所以一个错误的配置或错误的影响（即使是 jail 内的超级用户所做的）也不会危害到系统其他部分的完整性。由于在 jail 外实际上没有任何东西被修改，"变化 "可以通过删除 jail 的目录树副本而被丢弃。
然而 FreeBSD jail 并没有实现真正的虚拟化； 它不允许虚拟机运行不同于基本系统的内核版本。
FreeBSD jail 是提高服务器安全性的有效方法，因为 jail 环境与系统的其他部分(其他 jail 和基本系统)是分离的。
如果您想更好地了解 FreeBSD jail 和 Linux 容器之间的区别，请阅读博客文章 Setting the Record Straight: containers vs. Zones vs. Jails vs. VMs 。
FreeBSD 有 iocage 工具，它被设计用来简化 jail 管理任务。它将运行 VNET 或共享 IP 网络的 ZFS 支持的 jail 的管理抽象化。

Bastille
Bastille 是一个开源系统，用于在 FreeBSD 上自动部署和管理容器化应用程序。
Bastille 使用 FreeBSD jails 作为容器平台，并加入了模板自动化，以创建一个类似于 Docker 的容器化软件集合。
模板负责安装、配置、启用和启动软件，为构建容器化堆栈提供了一种自动化的方式。

Capsicum
Capsicum 是剑桥大学计算机实验室开发的一个沙盒框架，得到了 Google 、FreeBSD 基金会和 DARPA 的支持。Capsicum 扩展了 POSIX API，提供了一些新的操作系统基元，以支持类似 UNIX 操作系统上的对象能力安全。
Capabilities - 具有细粒度权限的精炼文件描述符
能力模式--拒绝访问全局命名空间的进程沙盒。
流程描述符--以能力为中心的流程 ID 替换
匿名共享内存对象--POSIX 共享内存 API 的扩展，支持与文件描述符相关的匿名交换对象（能力）。
rtld-elf-cap - 修改 ELF 运行时链接器，以构建沙盒应用。
libcapsicum - 用于创建和使用功能和沙盒组件的库。
libuserangel - 允许沙盒应用程序或组件与用户天使（如 Power Boxes ）交互的库。
chromium-capsicum - Google 的 Chromium 网页浏览器的一个版本，它使用能力模式和能力来为高风险的网页渲染提供有效的沙盒。
Capsicum 的 FreeBSD 实现，由 Robert Watson 和 Jonathan Anderson 开发，在 FreeBSD 10.0 中开箱即用。Capsicum for FreeBSD 是一个参考实现，它不仅可以作为 Capsicum API 和语义的参考，而且还为移植到其他平台提供了起点源代码 (例如，Capsicum for Linux 和 Capsicum for DragonFlyBSD)。

DTrace
DTrace 是一个从 Solaris 移植过来的综合性动态跟踪框架。DTrace 提供了一个强大的基础架构，允许管理员、开发人员和服务人员简明扼要地回答有关操作系统和用户程序行为的任意问题。
DTrace 可以提供正在运行的系统的全局概览，例如活动进程所使用的内存量、CPU 时间、文件系统和网络资源。DTrace 还可以提供细粒度的信息，如调用特定函数的参数日志，或访问特定文件的进程列表。
有关 DTrace 使用的更多信息，请参阅 DTrace 单行本教程和 DTrace 示例。
在 Hacker News 上也有一个有趣的讨论，其中有许多关于 DTrace for Linux 的相关评论。

bhyve
bhyve 是一个原生的 FreeBSD 虚拟机管理程序，它可以在虚拟机中运行客体操作系统。可以通过命令行参数来指定虚拟 CPU 的数量、客体内存的数量和 I/O 连接等参数。
bhyve 支持多种客体操作系统的虚拟化，包括 FreeBSD 9+、OpenBSD 、NetBSD 、Linux 、illumos 、DragonFly 、Windows Vista 及更高版本和 Windows Server 2008 及更高版本。目前的开发工作旨在扩大对 x86-64 架构的其他操作系统的支持。
bhyve 管理程序在 FreeBSD 10.0-RELEASE 中成为基础系统的一部分。
bhyve 要求处理器支持 Intel Extended Page Tables (EPT) 或 AMD Rapid Virtualization Indexing (RVI) 或 Nested Page Tables (NPT)。使用多于一个 vCPU 的 Linux 客座或 FreeBSD 客座，需要 VMX 无限制模式支持（ UG ）。较新的处理器，特别是英特尔酷睿 i3/i5/i7 和英特尔至强 E3/E5/E7，支持这些功能。UG 支持是随着英特尔的 Westmere 微架构引入的。

防火墙
FreeBSD 的基本系统中内置了三种不同的防火墙。PF, IPFW, 和 IPFILTER, 也就是 IPF.
从 FreeBSD 5.3 开始，OpenBSD 的 PF 防火墙被移植到了基本系统中。PF 是一个完整的、全功能的防火墙，它可以选择支持 ALTQ (Alternate Queuing)，提供服务质量 (QoS)。PF 的过滤语法与 IPF 类似，但做了一些修改，使其更加清晰。网络地址转换（ NAT ）和服务质量（ QoS ）已经集成到 PF 中，QoS 通过导入 ALTQ 排队软件，并与 PF 的配置联系起来。此外，还扩展了 PF 的功能，如用于故障转移和冗余的 pfsync 和 CARP，用于会话认证的 authpf，以及用于缓解防火墙困难的 FTP 协议的 ftp-proxy 等。同时，PF 还支持 SMP （对称多处理）&STO （状态跟踪选项）。
PF 的日志记录是众多创新功能之一。PF 的日志记录是可以在 pf.conf 中按规则配置的，日志由 PF 通过一个名为 pflog 的伪网络接口提供，这是用户级程序从内核级模式中提取数据的唯一方式。日志可以使用标准的实用程序（如 tcpdump ）来监控。
IPFW 是为 FreeBSD 编写的状态防火墙，它同时支持 IPv4 和 IPv6 。它由以下几个组件组成： 内核防火墙过滤规则处理器及其集成的数据包统计工具、日志记录工具、NAT 、dummynet 流量转换工具、转发工具、桥接工具和 ipstealth 工具。
FreeBSD 在 /etc/rc.firewall 中提供了一个示例规则集，它定义了几种常见场景下的防火墙类型，以帮助新手用户生成合适的规则集。IPFW 提供了强大的语法，高级用户可以使用它来制作满足特定环境安全要求的自定义规则集。
IPF 是一个跨平台的开源防火墙，已经被移植到多个操作系统上，包括 FreeBSD 、NetBSD 、OpenBSD 和 Solaris 。IPF 是一个内核侧的防火墙和 NAT 机制，可以被用户国程序控制和监控。防火墙规则可以用 ipf 设置或删除，NAT 规则可以用 ipnat 设置或删除，IPF 内核部分的运行时统计可以用 ipfstat 打印，ipmon 可以用来将 IPF 的操作记录到系统日志文件中。
IPF 最初是采用 "最后匹配的规则获胜 "的规则处理逻辑编写的，只使用无状态规则。此后，IPF 得到了增强，加入了快速和保持状态选项。

调整
FreeBSD 有超过五百个系统变量可以通过 sysctl 工具来读取和设置。这些系统变量可以用来对运行中的 FreeBSD 系统进行修改，其中包括 TCP/IP 协议栈和虚拟内存系统的许多高级选项。这其中包括许多 TCP/IP 协议栈和虚拟内存系统的高级选项，对于有经验的系统管理员来说，这些选项可以显著地提高系统的性能。

GEOM
FreeBSD GEOM 是 FreeBSD 操作系统的主要存储框架。它提供了一种标准化的方式来访问存储层。GEOM 是模块化的，允许 GEOM 模块连接到框架中。例如，geom_mirror 模块为系统提供了 RAID1 或镜像功能。目前已经有很多模块可以使用，而且 FreeBSD 的各个开发者也一直在积极开发新的模块。
由于 GEOM 的模块化设计，模块可以堆叠在一起，形成一个 GEOM 层链。例如，在 geom_mirror 模块的基础上，可以添加一个加密模块，如 geom_eli 来提供一个镜像和加密的卷。每个模块都有消费者和提供者。提供者是 geom 模块的源头，通常是一个物理硬盘，但有时也是一个虚拟化的磁盘，如内存盘。geom 模块又提供一个输出设备。其他 GEOM 模块，也就是所谓的消费者，可以使用这个提供者来创建一个相互连接的模块链。

Linux 二进制兼容性
FreeBSD 提供了与 Linux 的二进制兼容。这使得用户可以在 FreeBSD 系统上安装和运行许多 Linux 二进制文件， 而无需首先修改二进制文件。在某些特定情况下，Linux 二进制文件在 FreeBSD 上的表现甚至比在 Linux 上的表现更好。
并非所有 Linux 特定的操作系统功能都能在 FreeBSD 上得到支持。例如，如果 Linux 二进制文件过度使用 i386 的特定调用，例如启用虚拟 8086 模式，那么它们将无法在 FreeBSD 上运行。

安全事件审计
FreeBSD 包含对安全事件审计的支持。事件审计支持对各种与安全相关的系统事件进行可靠、精细和可配置的记录，包括登录、配置更改、文件和网络访问。这些日志记录对于实时系统监控、入侵检测和事后分析都是非常宝贵的。FreeBSD 实现了 Sun 发布的 Basic Security Module (BSM) 应用编程接口 (API) 和文件格式， 并可与 Solaris 和 MacOS 的审计实现互操作。

最后说明
这篇文章并没有详尽地列出使用 FreeBSD 而不是 GNU/Linux 的技术原因。还有许多其他的原因我没有提及。然而，这些是我个人认为最突出的一些特性。
除非您有非常特殊的需求，例如对硬件的特殊支持，否则当您运行和管理 FreeBSD 时，您通常会体验到更大的整体感、控制感和和谐感。
您在使用 FreeBSD 时可能会遇到的问题是缺乏硬件支持的情况，或者是特定的第三方应用程序非常以 Linux 为中心的情况。后者主要与桌面应用程序有关，而不是服务器应用程序。
例如，Mozilla 开发 Firefox 时，主要关注的是 Linux 、OSX 和 Windows 。这些被称为 Tier-1 平台。FreeBSD 、OpenBSD 、NetBSD 和 Solaris 作为 Tier-3 平台位于支持列表的底部。Mozilla 开发人员无法可靠地访问非 Tier-1 平台或构建环境。在任何时候，从 mozilla-central 为非 Tier-1 平台构建的 Firefox 都可能无法正常运行或根本无法构建。Tier-3 平台有一个维护者或社区，他们试图保持平台的工作。这些平台不受 Mozilla 的持续集成过程的支持，Mozilla 也不会在这些平台上进行例行测试。
这意味着 FreeBSD 的维护者必须花费额外的时间来确保像 Firefox 这样的应用程序能够在 FreeBSD 上编译和运行。而且当出现问题时，Mozilla 的开发人员往往不会像在 Linux 、Windows 或 OSX 上出现问题时那样关注这些问题。其他以 Linux 为中心的第三方应用程序也是如此。
这并不意味着这些应用程序不能在 FreeBSD 上运行，只是意味着您偶尔会遇到一些问题。例如，当我写这篇文章的时候，Micro 编辑器出现了一个问题，当你试图用 Alt-g 打开菜单时，它在 FreeBSD 上崩溃了。这个问题在 Linux 上并不存在。
我在服务器和桌面工作站上都使用 FreeBSD，最近我把在 Debian GNU/Linux 和 Arch Linux 上运行 ZFS 的系统迁移到了 FreeBSD 。由于 FreeBSD 为 ZFS 提供了更好的集成，我不仅体验到了性能的提升，也体验到了可靠性的提升。
我的一个主要工作站运行的是使用 i3 作为窗口管理器的 FreeBSD 。我有一个相同的设置，在同一台机器上用不同的硬盘运行 Arch Linux 。从纯粹的桌面使用角度来看，您看不出任何区别，也没有任何理由将 Arch Linux 作为桌面操作系统而不是 FreeBSD，无论是从性能上、从简单性上还是从任何其他原因来看 -- 唯一的例外是，如果您有不支持的硬件。
FreeBSD 没有像 GNU/Linux 那样得到同样的关注，实在是一个遗憾。在很多情况下，尤其是在生产服务器和商业用途上，一个公司运行 FreeBSD 而不是 Linux 可以获得很多好处，而他们运行 Linux 的唯一原因往往是出于习惯和对 FreeBSD 缺乏了解。
下一次当您需要部署一个新的系统时，我建议您也调查和测试一下 FreeBSD 。它是非常值得您花时间的。

原文地址： https://unixsheikh.com/index.html
