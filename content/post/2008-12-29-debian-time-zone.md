---
title: Debian下调整时间[转]
author: 黄俭
date: '2008-12-29'
slug: debian-time-zone
categories:
  - Computer
tags:
  - Linux
---
转自[这里](http://hi.baidu.com/somelog/blog/item/f688e1a861bf64b4ca130c2b.html)

先说时区的配置。以前Debian有个好胜的时区配置工具，叫tzconfig，现在也没有
了。但配置时区倒也简单，主要是两个文件：

```bash
/etc/localtime
/etc/timezone
```

timezone这个文件是个文本，里面只需要写一行自己的时区就行，我们这里就是上
海，Asia/Shanghai（谁知道为什么不是北京呢？）。 localtime这个文件的类型
不清楚，里面就写了些timezone data，它可以从系统自带时区文件那里拷贝，位
置在：

>/usr/share/zoneinfo

从这个目录下找到Shanghai拷贝到/etc下的localtime即可。有人说建个连接也可
，这样还可以保证系统数据有变化时不必再管。

设定了时区，还要确定Linux的时间方案。Linux支持UTC时间，Coordinated
Universal Time，也就是世界协调时，也就是本初子午线上的时间，它和以前的格
林威治标准时（GMT）的区别似乎是它是由多个原子钟平均出来的。在
/etc/default/rcS这个文件中，设定了系统是否使用UTC，UTC=yes就是用。

计算机自己还有自己的时间，也就是硬件时间，hard clock，也就是存在BIOS里那
个时间，关机也不会丢失。计算机启动时，就要读取这个时间。这个时间如果设定
为UTC（GMT），也就是伦敦那地方的时间，就要在rcS文件中设定UTC=yes，反之则
要设为no。

总之就是两种正确的设置：

>BIOS=本地时间，UTC=no

>BIOS=UTC时间，UTC=yes

一般来讲，BIOS里面都设定为当地时间，这是因为如果装双系统的话，Windows似
乎不懂utc，就会出问题。这时UTC=no。

如果一切顺利，到这时，进入Linux之后显示的时间应该是正确的了。但不少人的
机器，包括这回这台640m，仍旧不正确，而是比正确时间再往前跑了8小时。这里
的问题出在Linux读取硬件时间上了。

Linux读取这个硬件时间要用到hwclock这个命令：

hwclock –show ：显示硬件时间
hwclock –systohc ：将系统时间写入硬件
hwclock –hctosys ：将硬件时间写入系统时间

在出问题的时候，hwclock 这一组命令的运行通常是不能成功的，错误经常是这样
的：

select() to /dev/rtc to wait for clock tick timed out

也就是不能读取/dev/rtc，也就是硬件时间。这又是因为某些机器的BIOS处理方式
和Linux的rtc内核模块之间出现了问题。

Linux又有3个这类模块，rtc/genrtc/rtc_dev，似乎是一个比一个新，而debian通
常自己用的是rtc这个老模块；但 Dell/ibm/acer等等厂商现在都可能使用新的
BIOS，这种BIOS和这个rtc就可能不对付。如果出现了上面那个timeout的问题，有
两种方法可以解决：

1, 给hwclock加参数，–directisa，也就是：

hwclock –directisa –show

如果运行成功，说明这个办法可行。则把此参数添加为hwclock的缺省参数即可。
在debian 4.0之后，可以直接在/etc/default/rcS中添加一行：

HWCLOCKPARS=”–directisa“

而在4.0以前，可能只能在hwclock启动脚本中添加，/etc/init.d/hwclock.sh，把
里面的”/sbin/hwclock“ 全部替换为 ”/sbin/hwclock –directisa”。现在在
debian sid中，这个脚本的第一行其实是HWCLOCKPARS=，也可以像rcS一样添加参
数了。

2, 换用其他内核rtc模块，用如下方法测试哪个模块好用：

```shell
# modprobe rtc
# hwclock –show
# rmmod rtc
# modprobe genrtc
# hwclock –show
# rmmod genrtc
# modprobe rtc_dev
# hwclock –show
# rmmod rtc_dev
```

没有显示time out的就是好用的了，然后可以在blacklist中阻止不好用的，在
modules里面加上好用的那个。

用完这两个方法，hwclock应该能直接工作了，也就是可以读取硬件时间了。再配
上utc设置正确，重启之后时间就是对的了。

为了让BIOS时间更准确，除了可以找个精确的时间源，比如CDMA手机或是GPS，靠
自己的手指来精确设定BIOS时间之外，还可以用hwclock把准确的时间写入BIOS。
前一种方法细心点可以做到几秒误差，而后一种怎么也在1秒以下了。

安装ntpdate这个包，它可以从时间服务器上读取到正确的时间，精度还是很高的
：
aptitude install ntpdate
ntpdate pool.ntp.org

此时系统时间就已经是ntp的时间了，相当精确，把它写入硬件：

hwclock –systohc

这样BIOS时间也就很准了。以后开机没网络，没办法运行ntpdate的时候也都是准
的。