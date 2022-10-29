Welcome to Lean's  git source of  Gargoyle and packages

中文：如何编译自己需要的 石像鬼 Gargoyle 固件

默认双界面，80 是石像鬼，8080 是 luci，中文界面，默认密码为 password

编译命令如下:

1. 首先装好 Ubuntu 64bit，推荐  Ubuntu  14 LTS x64

2. 命令行输入 sudo apt-get update ，然后输入
sudo apt-get install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev

3. git clone https://github.com/coolsnowwolf/gargoyle 命令下载好源代码，然后 cd gargoyle 进入目录

4. ./scripts/feeds update -a 
   ./scripts/feeds install -a
   make menuconfig 

5. 最后选好你要的路由，输入 make -j1 V=s （-j1 后面是线程数。第一次编译推荐用单线程，国内请尽量全局科学上网）即可开始编译你要的固件了。

本套代码保证肯定可以编译成功。里面包括了 R7.5 所有源代码，包括 IPK 的。

你可以自由使用，但源码编译二次发布请注明我的 GitHub 仓库链接。谢谢合作！

特别提示：
1. 源代码中绝不含任何后门和可以监控或者劫持你的 HTTPS 的闭源软件，SSL 安全是互联网最后的壁垒。安全干净才是固件应该做到的。
2.如果你自认为 Koolshare 论坛或者其固件的脑残粉，本人不欢迎你使用本源代码。所以如果你是，那么使用过程中遇到任何问题本人概不回应。
3.如有问题需要讨论，欢迎加入 QQ 讨论群：Gargoyle OpenWrt 编译大群 ,号码 610530025 ，加群链接 https://jq.qq.com/?_wv=1027&k=5eA89Wv

Please use "make menuconfig" to choose your preferred
configuration for the toolchain and firmware.

You need to have installed gcc, binutils, bzip2, flex, python, perl, make,
find, grep, diff, unzip, gawk, getopt, subversion, libz-dev and libc headers.

Run "./scripts/feeds update -a" to get all the latest package definitions
defined in feeds.conf / feeds.conf.default respectively
and "./scripts/feeds install -a" to install symlinks of all of them into
package/feeds/.

Use "make menuconfig" to configure your image.

Simply running "make" will build your firmware.
It will download all sources, build the cross-compile toolchain, 
the kernel and all choosen applications.

To build your own firmware you need to have access to a Linux, BSD or MacOSX system
(case-sensitive filesystem required). Cygwin will not be supported because of
the lack of case sensitiveness in the file system.



Note: Addition Lean's private package source code in ./package/lean directory. Use it under GPL v3.

GPLv3 is compatible with more licenses than GPLv2: it allows you to make combinations with code that has specific kinds of additional requirements that are not in GPLv3 itself. Section 7 has more information about this, including the list of additional requirements that are permitted.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Gargoyle Router Management Utility

Gargoyle is a third party firmware for routers based on the Openwrt firmware. It can be described at a high level as a front-end to Openwrt, however there are several packages and custom kernel modules which are not included upstream in Openwrt. As a result, Gargoyle cannot be installed as a set-of-packages to an existing Openwrt installation, and is a separate firmware as far as installation is concerned.
Gargoyle is open-source software, and aims to be the first open-source firmware project to place a strong focus on creating a user-friendly interface.

## Getting Started

As a developer, or even a casual contributor, you should start [here](https://www.gargoyle-router.com/wiki/doku.php?id=developer_info) at the Gargoyle wiki developer documentation.
You should always consult the wiki for up to date information on getting started (as it is maintained by the community, and this readme may not receive as much attention), however as a brief summary...

### Prerequisites

The following prerequisites assume a 64bit Ubuntu system. Many devs use virtual machines, and they are perfectly fine for this kind of work.

```
sudo apt-get install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo npm
```

**NOTE** Python is also required and needs to be in your path. Python 3 is recommended. For Ubuntu users, it is recommended to install `python-is-python3` to solve this issue automatically.

### Get the source

You've already found it if you're reading this, but lets get it on your local machine. Choose one of the following commands depending on whether you want to use SSH or HTTPS authentication:

```
git@github.com:ericpaulbishop/gargoyle.git
https://github.com/ericpaulbishop/gargoyle.git
```

Then

```
cd gargoyle
```


## Building Gargoyle

After building is complete, you'll have <target>-src/, built/<target> and images/<target> folders. Retrieve your compiled firmwares from images, and the packages from built.

### Make all targets

```
make FULL_BUILD=true
```

### Make a single target (e.g. ar71xx)

```
make ar71xx FULL_BUILD=true
```

### Make a single profile (e.g. ar71xx.usb_large)

```
make ar71xx.usb_large FULL_BUILD=true
```

### Make a single target (e.g. ar71xx) without rebuilding Openwrt (just packages)

```
make ar71xx
```

### Make a custom target

See the wiki for more detailed instructions.

```
make custom
```

## Install

Please see the relevant Openwrt wiki or ToH entries for your device for the intricacies of installation, upgrading and failsafe for your device.

## Where do I get help?

The forums: [Gargoyle-Router Forums](https://www.gargoyle-router.com/phpbb/index.php)

## Contributing

Please read [CONTRIBUTING.md](https://github.com/ericpaulbishop/gargoyle/blob/master/CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## Reporting an issue or bug

If you have discovered a genuine bug or other shortcoming in the firmware that you would like addressed, please first check the forums to see if it has already been raised and addressed. If the community is not able to address it for you, or the consensus is that it is a genuine bug, please raise an issue in GitHub.
**NOTE** Issues are not the place for feature requests. Please keep these to the forum.
Include as much detail as you can, such as:
* Gargoyle Version
* Router Make, Model and Version
* What were you doing when the bug occurred?
* What happened (what's the bug)?
* What did you expect to happen (what is your expectation of the proper behaviour)?
* Can you reproduce the bug everytime, sometimes, rarely? (For rare issues, start with the forums and see if others are seeing the same issue)
* Exact steps to reproduce the bug

## License

Gargoyle is copyright (C) 2008-2019 by Eric Bishop
Gargoyle is free software; you can redistribute it and/or modify it under the terms of the [GNU General Public License version 2.0](http://www.gnu.org/licenses/gpl-2.0.html) as published by the Free Software Foundation, with the following clarificaiton/exception that permits adpating the program to configure proprietary "back end" software provided that all modifications to the web interface portion remain covered by this license:

> The GNU General Public License (GPL) is vague as to what constitutes “mere aggregation” under section 2, and what contitutes a work “based on the Program.” In the special case in which the Program is modified for the purpose of configuring other (potentially GPL-incompatible) software, the combination of the Program and this other software shall be considered "mere aggregation" if and only if the ONLY interaction between the Program and the other software being configured takes place via CGI (Common Gateway Interface) scripts and/or programs. However, these CGI scripts/programs as well as any other additions and modifications necessary for the configuration of the other software shall be considered “based on the Program” for the purposes of this license. Further, if any portion of the Program is used as part of an interface that can be rendered via a web browser, all portions of that interface that can be rendered via a web browser (including, but not limited to, javascript, svg/ecmascript, css, html, and shell/perl/php/other cgi scripts) shall be considered “based on the Program.”
> This clarification/exception shall apply to the license of all derived works, and must appear in all relevant documentation. If you choose to release your modification to the Program under a later version of the GPL that directly contridicts this clarification/exception, this clarification/exception shall supersede any contradictory language in that version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

## Acknowledgments

* Eric Bishop - Project founder and lead developer
* The community - For using, supporting and contributing to Gargoyle
