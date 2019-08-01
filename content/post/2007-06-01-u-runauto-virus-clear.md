---
title: 删除U盘上的runauto…[转载]
author: 黄俭
date: '2007-06-01'
slug: u-runauto-virus-clear
categories:
  - Computer
tags:
  - Health
---
现在在u盘上经常看到一个病毒文件runauto..(隐藏属性），用正常的删除方法的无法删除的，很多人会选择格式化u盘，但这样能盘的使用寿命有一样影响，而且不方便。

好了，以下对这个文件进行分析：

　其实该文件夹是由dos创建的，全名应该为runauto…说到这里你应该知道为什么不能删了吧。

　　这样删的方法好易了：（以 D 盘为例）
开始——运行——输入“cmd”——输入“D: ”——输入“rd /s/q runauto…\ ”

2.无法删除”runauto..”文件夹。
解决方法：该文件夹真正的名称为”runauto…\” 执行RMDIR C:\runauto…\ /S /Q即可删除。

3.我写了一个专门的批处理命令行来删除所有的文件：

```shell
——————–命令行工具开始——————–
@echo off
echo “先中止病毒进程”
NET STOP “Kerberos Key Distribution Centers”

echo “删除C盘病毒文件”
DEL C:\WINDOWS\lsass.exe /F /Q /A R H S A
DEL C:\WINDOWS\setuprs1.pif /F /Q /A R H S A
DEL C:\WINDOWS\cmd.exe.exe /F /Q /A R H S A
DEL C:\WINDOWS\regedit.exe.exe /F /Q /A R H S A
DEL C:\WINDOWS\r.exe /F /Q /A R H S A

echo “删除各个分区根目录下文件，需要根据各个电脑的分区数量进行调整”
RMDIR C:\runauto…\ /S /Q
DEL C:\autorun.* /F /Q /A R H S A
RMDIR D:\runauto…\ /S /Q
DEL D:\autorun.* /F /Q /A R H S A
RMDIR E:\runauto…\ /S /Q
DEL E:\autorun.* /F /Q /A R H S A
RMDIR F:\runauto…\ /S /Q
DEL F:\autorun.* /F /Q /A R H S A
RMDIR G:\runauto…\ /S /Q
DEL G:\autorun.* /F /Q /A R H S A

COPY C:\WINDOWS\regedit.exe C:\WINDOWS\ghregedi.exe
echo “注册表编辑器已备份为ghregedi.exe”

COPY C:\WINDOWS\SYSTEM32\cmd.exe C:\WINDOWS\SYSTEM32\ghcmd.exe
echo “命令行工具已备份为ghcmd.exe”

echo “文件删除完毕，请重新启动并清理注册表相关项。”

——————–命令行工具结束——————–
```

新建一个记事本文档，把分割线之间的内容复制进去（不包括分割线），另存为123.bat然后执行即可。