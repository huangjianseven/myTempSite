---
title: 手动清除一个木马
author: 黄俭
date: '2007-03-31'
slug: Clear-Trojan-horse
categories:
  - Computer
tags:
  - programming
---
昨天，我发现只要我的电脑一打开IE，就会有一个隐藏的进程会偷偷地从广东汕头电信的一个IP的80端口下载一些盗号的程序，这些程序会被我的杀毒程序Macfee所发现，但是这个隐藏进程并不能被Macfin所发现，换了Nod32也还是不行。

另外，在关机或重启的时候，有一个对话框，老是说tianlia.exe无法关闭，要手动点“立即结束”才能关机或重启。

后来我换了Antivir，发现当我启动命令提示符或IE的时候，Antivir会提示发现病毒，该信息指向C:\Program Files\Common Files\Microsoft Shared\MSInfo\目录下一个叫newinfo.dll的文件。

这下我明白了，这个动态链接库在cmd或IE启动时会被加载，而一个病毒也在此时启动了!!!!!

于是我在安全模式下，试图删除此动态链接库文件，失败。于是灵机一动，把Antivir的运行级别改高一点，扫描本文中提到的那个目录，提示找到newinfo.dll为病毒，这时我在交互窗口中选择rename，哈哈，重命名了。

再扫描，选择delete，Antivir提示重启之后即可删除。于是重启再进入安全模式，果然该文件被清除了。

正常启动Windows，一切恢复正常。