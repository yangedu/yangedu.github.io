---
layout: post
title: Centos配置ftp服务端及配置用户
category: 服务器
tags: 总结
keywords: centos,ftp
description: 服务器配置ftp服务端功能
---

### 本文测试环境   
1. CentOS 7 
2. 测试服务器IP 192.168.1.170

### 安装并启动 FTP 服务

1.1 安装 VSFTPD

使用 yum 安装 vsftpd

yum install -y vsftpd  

1.2 启动 VSFTPD

安装完成后，启动 FTP 服务：  
service vsftpd start  

启动后，可以看到系统已经监听了 21 端口：  
netstat -nltp | grep 21  
此时，访问 ftp://192.168.1.170 可浏览机器上的 /var/ftp目录了。

### 配置 FTP 权限

2.1 了解 VSFTP 配置

vsftpd 的配置目录为 /etc/vsftpd，包含下列的配置文件：

vsftpd.conf 为主要配置文件  
ftpusers 配置禁止访问 FTP 服务器的用户列表  
user_list 配置用户访问控制  

2.2 阻止匿名访问和切换根目录

匿名访问和切换根目录都会给服务器带来安全风险，我们把这两个功能关闭。

编辑 /etc/vsftpd/vsftpd.conf，找到下面两处配置并修改：
 
禁用匿名用户  12行 YES 改为NO  
anonymous_enable=NO

禁止切换根目录 101 行 删除#  
chroot_local_user=YES  

编辑完成后保存配置，重新启动 FTP 服务  
> service vsftpd restart

2.3 创建 FTP 用户  
创建一个用户 ftpuser  
> useradd ftpuser

为用户 ftpuser 设置密码  
密码：123456 用户名ftpuser  
> echo "123456" | passwd ftpuser --stdin  

2.4 限制该用户仅能通过 FTP 访问

限制用户 ftpuser只能通过 FTP 访问服务器，而不能直接登录服务器：

usermod -s /sbin/nologin ftpuser  

2.5 为用户分配主目录

为用户 ftpuser创建主目录并约定：

/data/ftp 为主目录, 该目录不可上传文件  

/data/ftp/pub 文件只能上传到该目录下  

在/data中创建相关的目录  

mkdir -p /data/ftp/pub  

2.5.1 创建登录欢迎文件
 
echo "Welcome to use FTP service." > /data/ftp/welcome.txt  

2.5.2 设置访问权限

chmod a-w /data/ftp && chmod 777 -R /data/ftp/pub

设置为用户的主目录：  
usermod -d /data/ftp ftpuser

### 访问FTP

根据您个人的工作环境，选择一种方式来访问已经搭建的 FTP 服务

注意：记得关闭防火墙或者开放FTP默认端口(21)

 关闭SELinux服务
setenforce 0 
 关闭防火墙
iptables -F 
通过 Windows 资源管理器访问
Windows 用户可以复制下面的链接 
到资源管理器的地址栏访问：  
ftp://ftpuser:javen205@192.168.1.170 
其中ftpuser为登录FTP的用户名，javen205为登录FTP的密码  

### 部分走过的坑  
> 1. 如果使用的腾讯云空间，需要先设置 安全组 开放21，20端口。（21ftp链接服务器，20访问查看文件夹）。  
不开放20端口，返回连接上服务器，等待目录列表而无法打开列表。   
本地ftp配置选择主动连接。  
>  
> 2. 如果主目录和允许操作的目录为同一个文件夹，需要在ftp配置文件里增加  
allow_writeable_chroot=YES  
允许在根目录中读写