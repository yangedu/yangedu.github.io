---
layout: post
title:  "Ubuntu 服务器环境配置"
date:   2017-10-31 14:10:51 +0800
categories: 服务器
tags: 总结
author: 葩木乐
description: 服务器环境配置总结
---
一直想学学linux环境，之前一个同事说学习这个的最好办法就是，强制使用这个系统，不要再依赖win系统了。  
今天就把linux系统在虚拟机上装了下，然后各种百度，配置了下php的环境。  
注意：由于查找资料时会有各种方法问题，并且随时间的推进，有些可能不在适用，可能有的环境不再适用，具体的还是得根据自己的环境来处理。
本文档整理时间是2017-10-31。

> linux版本：Ubuntu 16.04.3 LTS ( GUN/Linux 4.4.0-87-generic x86_64 )  

### 本地可以通过ip访问到虚拟机系统
 在虚拟机上装上linux系统就不多写了，基本是下一步下一步。不过可以把虚拟机的打印机，声音这些去掉。  
 虚拟机的网络连接方式为 NAT模式（N) 用于共享主机的ip地址。（这里这么配置是因为在公司里，ip地址都是分配的
 不允许增加ip地址，就选择了共享ip，如果是在足够宽裕的环境，可以选择有独立ip的桥接模式（没测试，请自测）。  
 
 登录虚拟机，查看虚拟机ip  
 ````
ifconfig
````
获取到ip,打开本地网络设置，修改网络连接，找到VMware Network Adapter VMnet8这个网卡，修改ip4地址就行  
如我的虚拟机ip地址是192.168.177.129，在实体机vm这个网卡上设置的ip地址是192.168.177.1，子网掩码默认的就行。    
[参考](http://www.linuxidc.com/Linux/2015-05/117048.htm) 网址  

### 更新服务器资源包  
 ```
  sudo apt-get update 
 ```  
### 安装apache 
 ````
 sudo apt-get install apache2
 ````
 装好之后可以访问服务器ip查看默认页面。[ 我的是192.168.177.129 ]。  
 也可以代码查看apache安装地址，版本信息  
 ````
 whereis apache2
 apachectl -v
 ````  
 
### 安装php7
 （复制的代码，可能模块不全，以后还得补)  
 ````
 sudo apt-get install php7.0 php7.0-cli php7.0-fpm php7.0-gd php7.0-json php7.0-mysql php7.0-readline
 ````
> 重点注意情况： 
此时是无法解析php网页的，因为没有安装apache php module  
````
sudo apt-get install libapache2-mod-php7.0
````  
测试php是否正常运行  
````
sudo mv /var/www/html/index.html /var/www/html/index.html.bak 
sudo echo “<?php phpinfo();?>” > /var/www/html/index.php 
sudo service apache2 restart
````  
访问根目录，应该出现服务器apahce2,php等配置信息。 

### 安装mysql
````
sudo apt-get install mysql-server
安装过程中MySQL要求设定账户有密码
````
安装相关模块  
````
sudo apt-get install libapache2-mod-auth-mysql php5-mysql

安装完成后重启apache：
sudo /etc/init.d/apache2 restart
````
### 安装phpmyadmin
````
sudo apt-get install phpmyadmin 
安装完成后访问：http://localhost/phpmyadmin/，提示not found。还需要把安装好的phpmyadmin文件夹放入/var/www/。

sudo ln -s /usr/share/phpmyadmin/ /var/www/
或者将phpmyadmin直接复制到/var/www。
````
到此，服务器配置基本完成，现在在浏览器里访问虚拟机的ip就可以访问到服务器了。

### 域名配置
在服务上配置对应的解析域名，当域名指向该服务器时就能正常访问了。  
本地的设置方法: 修改host，添加一个虚拟域名，如abc.ywf 指向虚拟机的ip就可以了。

### 参考
>  http://blog.csdn.net/u011728480/article/details/52316664  
http://blog.csdn.net/yeyuangen/article/details/52103445  
https://jingyan.baidu.com/article/dca1fa6fadc61ff1a5405244.html  
http://www.cnblogs.com/boshen-hzb/p/5889633.html