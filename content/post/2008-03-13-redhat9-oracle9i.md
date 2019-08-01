---
title: Redhat9.0下安装oracle9i
author: 黄俭
date: '2008-03-13'
slug: redhat9-oracle9i
categories:
  - Computer
tags:
  - Linux
---
之前在Redhat下成功安装了这个庞大的数据库管理系统，现在写一点东东，以资备忘。
先把主要参考文献列一下：

[第一篇](http://blog.csdn.net/daryl715/archive/2006/12/19/1448513.aspx)

[第二篇](http://jed.dzhope.com/read.php?24)

[第三篇](http://bbs.linuxeden.com/archiver/tid-100159.html)

下面有些内容是复制自上述文献。

1. 创建用户和组：

    ```shell
     [roko@miniroko] su -

     [root@miniroko]# groupadd oinstall
     [root@miniroko]# groupadd dba
     [root@miniroko]# useradd -g oinstall -G dba oracle
     [root@miniroko]# passwd oracle
    ```

2. 准备文件目录：

    ```shell
     [root@miniroko]# mkdir -p /opt/ora9/product/9.2
     [root@miniroko]# mkdir /var/opt/oracle
     [root@miniroko]# chown oracle.dba /var/opt/oracle
     [root@miniroko]# chown -R oracle.dba /opt/ora9
    ```

3. 调节系统内核参数及安装支持软件包：
    - 首先用命令rpm -qa|grep compat 查看系统中是否安有以下几个软件包：

      ```shell
       compat-gcc-7.3-2.96.118.i386.rpm
       compat-libgcj-7.3-2.96.118.i386.rpm
       compat-libgcj-devel-7.3-2.96.118.i386.rpm
       nss_db-compat-2.2-20.i386.rpm
      ```
如果没有，请拿出你的安装盘，安装以上的包。不要用原文给的那个APT的东东，不熟的人遇上没有解决的依赖性问题的话，就特别讨厌。

    - 设置内核参数，调节信号灯及共享内存：

```shell
[root@miniroko]# echo 250 32000 100 128 > /proc/sys/kernel/sem
[root@miniroko]# echo 536870912 > /proc/sys/kernel/shmmax
[root@miniroko]# echo 4096 > /proc/sys/kernel/shmmni
[root@miniroko]# echo 2097152 > /proc/sys/kernel/shmall
[root@miniroko]# echo 65536 > /proc/sys/fs/file-max
[root@miniroko]# echo 1024 65000 > /proc/sys/net/ipv4/ip_local_port_range
```
当然为了一开机系统就能自动帮你设好这些参数，也可改动 /etc/sysctl.conf 这个文件，加入以下的语句：

```shell
kernel.shmmax = 536870912
kernel.shmmni = 4096
kernel.shmall = 2097152
kernel.sem = 250 32000 100 128
fs.file-max = 65536
net.ipv4.ip_local_port_range = 1024 65000
```

保存后，即可。建议关于net.ipv4.ip_local_port_range不要改动，可以用cat /proc/sys/net/ipv4/ip_local_port_range 看到红帽子对这个所定义的范围已经符合，而且端口范围比这个小。

   - 设置oracle对文件的要求：
编辑文件：/etc/security/limits.conf 加入以下语句：

```shell
oracle soft nofile 65536
oracle hard nofile 65536
oracle soft nproc 16384
oracle hard nproc 16384
```

这个需要重启后才能生效的。但是安装的时候无所谓了。

4. 设置oracle的系统环境：
以oracle用户的身份登录：
su oracle

```shell
cd ~
```

编辑它的.bashrc文件加入以的东东：

```bash
#oracle 9i
export ORACLE_BASE=/opt/ora9
export ORACLE_HOME=/opt/ora9/product/9.2
export PATH=$ORACLE_HOME/bin:$ORACLE_HOME/Apache/Apache/bin:$PATH
export ORACLE_OWNER=oracle
export ORACLE_SID=ora9i
export ORACLE_TERM=vt100
export LD_ASSUME_KERNEL=2.4.1
export THREADS_FLAG=native
export LD_LIBRARY_PATH=/opt/ora9/product/9.2/lib:$LD_LIBRARY_PATH
export PATH=/opt/ora9/product/9.2/bin:$PATH
#
# change this NLS settings to suit your country:
# example:
# german_germany.we8iso8859p15, american_america.we8iso8859p2 etc.
#
#export NLS_LANG=’croatian_croatia.ee8iso8859p2′ (注意这个东东把它注释掉，因为我们用的是中文系统。然而为了能够显示中文加入以下一行：
export LC=en_US
```

退出，将你下载的三个iso文件准备好。

5. 解压你下载的文件：
    - 新建一个目录：mkdir /mnt/Oracle
    - 将三个文件拷入新建的目录：cp ln_* /mnt/Oracle
    - 解压三个文件： 
    
  ```shell
     cd /mnt/Oracle
     gunzip gunzip lnx_920_disk1.cpio.gz
     gunzip lnx_920_disk2.cpio.gz
     gunzip lnx_920_disk3.cpio.gz
     cpio -idmv < lnx_920_disk1.cpio
     cpio -idmv < lnx_920_disk2.cpio
     cpio -idmv < lnx_920_disk3.cpio
  ```
    - 这个将生成三个文件夹：DISK1, DISK2, DISK3

    - 切换至root

```shell
# xhost +
```

   - 以oracle身份登录图形界面

   - 为了应对乱码问题，做以下工作：

``` shell
$ export LANG=C
$ export C_ALL=C

$ /mnt/Oracle/DSIK1/runInstall.sh
```

我安装过程中没有遇到文献中所说的错误，好奇怪。呵呵，是我运气好么？
不过我用的三个文件不是文献中说的那几个。

整个安装过程中就有两次弹出对话框，无非是让我以root用户的身份运行脚本，运行后点continue或者OK，就可以了。