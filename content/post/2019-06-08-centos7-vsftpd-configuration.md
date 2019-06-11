---
title: CentOS7中配置FTP服务
author: 黄俭
date: '2019-06-08'
slug: centos7-vsftpd-configuration
categories:
  - Work
tags:
  - computer
---
1. 在线安装vsftpd

    ```shell
    # yum -y install vsftpd
    ```

1. 修改配置文件

     ```shell
      # vim /etc/vsfptd/vsftpd.conf
     ```
   
1. 第一轮操作
    - 允许匿名用户登录
    
        ```bash
         anonymous_enable=YES  # 允许匿名用户登录
         
         local_enable=YES  # 允许本地用户登录
         
         write_enable=YES # 允许写操作
         
         listen=YES # ipv4监听模式开启
         
         listen_ipv6=NO # ipv6监听模式关闭
        ```
    - 去除SELinux的影响
       - 先查状态
       
        ```shell
         # getsebool -a | grep ftp
        ```
          显示结果
        
        ```bash
         ftpd_anon_write --> off
         ftpd_connect_all_unreserved --> off
         ftpd_connect_db --> off
         ftpd_full_access --> off # 将此项设为on
         ftpd_use_cifs --> off
         ftpd_use_fusefs --> off
         ftpd_use_nfs --> off
         ftpd_use_passive_mode --> off
         httpd_can_connect_ftp --> off
         httpd_enable_ftp_server --> off
         tftp_anon_write --> off
         tftp_home_dir --> off # 将此项设为on
        ```
      - 进行设置
      
         ```shell
          # setsebool -P allow_ftpd_full_access on
          # setsebool -P tftp_home_dir on
         ```
      - 再次确认
      
      ```shell
       # getsebool -a | grep ftp
      ```
        
1. 启动FTP服务并配置开机自启动

    ```shell
     # systemctl start vsftpd.service
     # systemctl enable vsftpd.service
    ```
1. 关闭系统防火墙

    ```shell
     # systemctl stop firewalld.service
    ```
    这时应该就可以正常访问FTP了。
    
1. 第二轮操作
    - 操作目的
       - 打开防火墙，同时为FTP的访问（读与写）开放端口
       - 另建用户，用以上传文件
    - 新建一用户，用户名为ftproot，并设置密码，资源目录位于/var/ftp/huang/
       
       ```shell
        # useradd -d /var/ftp/huang -g ftp -s /sbin/nologin ftproot
       ```
    - 防止pam过度验证
    
       ```shell
        # vim /etc/pam.d/vsftpd
       ```
       注释掉下面这一行
      
       ```bash
        # auth required pam_shells.so
       ```
    - 重启FTP服务，ftproot应该可以登录了
    
      ```shell
       # systemctl restart vsftpd.service
      ```
    - 将用户限制在其主目录
       
       ```bash
        chroot_local_user=YES
        chroot_list_enable=YES
        chroot_list_file=/etc/vsftpd/chroot_list
      ```
      将上面创建的ftproot添加到chroot_list中，让其成为例外，从而可以用它上传文件
      
    - 解决下面的错误
    
       ![](/post/2019-06-08-centos7-vsftpd-configuration_files/chroot_ftp_500_error.png)
       
    - 去除该用户目录的write权限就好了
        
           ```shell
            # chmod -R  a-w /var/ftp/huang/
           ```
           然后再新建一目录用以上传文件
           
           ```shell
            # mkdir /var/ftp/huang/EBook
            # chown ftproot:ftp Ebook/
           ```
    - 防火墙重新布置
    
       ```shell
        # systemctl start firewalld.service
        # firewall-cmd --zone=public --add-port=20-21/tcp --permanent
        # firewall-cmd --reload
       ```
       如此这般就可以在开启防火墙的时候访问FTP了，但用Windows的文件管理器或浏览器还是不能访问的，这时需要配置PASV模式。
       
    - 被动模式设置
       - 配置文件中的最后加入这几行
       
          ```bash
           pasv_enable=YES
           pasv_min_port=50000
           pasv_max_port=60000
          ```
       - 防火墙中再次开放50000-60000的端口，并重新加载防火墙策略，最后重启FTP服务，一切搞定
       
          ```shell
           # firewall-cmd --zone=public --add-port=50000-60000/tcp --permanent
           # firewall-cmd --reload
           # systemctl restart vsftpd
          ```
          
1. 我的配置文件
    - 点[这里](/post/2019-06-08-centos7-vsftpd-configuration_files/vsftpd.conf)下载