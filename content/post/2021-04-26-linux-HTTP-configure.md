---
title: Linux下HTTP服务器的配置
author: 黄俭
date: '2021-04-26'
slug: linux-HTTP-configure
categories:
  - Computer
tags:
  - Linux
---

1. 命令过程
    - 安装网页服务器apache
    
     ```shell
      # yum update
      # yum -y install httpd
     ```
    - 启动网页服务并关闭防火墙
    
     ```shell
      # systemctl starty httpd
      # systemctl stop firewalld.service
      # ss -ltpn
     ```
    - 进入网页资源目录并建立相册文件夹
    
     ```shell
      # cd /var/www/html
      # mkdir  gallery
     ```
     
    - 将相册的PHP源代码复制到上面建立的相册文件夹(unzip解压缩)
    
    - 修改网页服务器配置文件,加入对PHP的支持
    
     ```shell
      # vim /etc/httpd/conf/httpd.conf
      # systemctl restart httpd
     ```
    
    - 安装GD库
    
     ```shell
      # yum -y install php php-gd
      # systemctl restart httpd
     ```
    - 按提示修改相册文件夹的权限
    
     ```shell
      # chmod 777 data/
      # chmod 777 pictures/
      # chmod 777 /backup
     ```
    - 关闭SELINUX
    
     ```shell
      # vim /etc/selinux/config
     ```
     
    - 端口转发，修改IP地址
    
    - 配置防火墙，将网页服务被允许
    
     ```shell
      # firewall-cmd --zone=public  --add-port=80/tcp --permanent
      # firewall-cmd --reload
      # systemctl enable httpd
     ```