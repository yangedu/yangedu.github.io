---
layout: post
title:  "初学yii2遇到的各种坑"
date:   2017-12-1 22:29:51 +0800
categories: php
tags: 总结
author: 葩木乐
description: 设计数据库的一些原则信息
---  

> 忽然觉得，我总是对别人没有严格要求的原因是：我没有对自己要求严格的勇气。

初学yii2,遇到各种坑，也许以后能写各种项目时再回头看这些时，就是感觉这些问题太小儿科吧，不过，这也算是成长吧。  

### 1. 国际大坑 composer的破墙之法  
随着php升级到了7，各大框架都使用了composer这种方法来解决依赖关系，但是在大陆访问国际最大同性交友平台github上，总是 莫名其妙 的断线，或者超卡。呵呵吧，现在能访问还不感恩！  
症状：通过composer安装yii2下载速度超慢，或者根本找不到资源包。  
解决：修改 composer 的全局配置文件，建立中国境内镜像  
打开命令行窗口（windows用户）或控制台（Linux、Mac 用户）并执行如下命令：
~~~ 
composer config -g repo.packagist composer https://packagist.phpcomposer.com  
~~~  
其他方法参见 https://pkg.phpcomposer.com/  

### 2.composer 找不到资源情况二  
症状：下载时提示各种找不到资源，或错误。  
解决：1. composer 需要安装 Composer Asset插件  
~~~
hp composer.phar global require "fxp/composer-asset-plugin:^1.2.0"
~~~  
2. 也许composer不是最新版本，请先更新到最新版  
~~~
composer selfupdate
~~~

### 3.资源包下载不下来  
通过 yiichina 下载页面（http://www.yiichina.com/download）操作步骤通过composer下载，总是下载失败，他们提供的语句：  
~~~
php composer.phar create-project yiisoft/yii2-app-advanced advanced 2.0.12  
~~~  

后来在其他入门教程里找到的其他语句能正常下载  
~~~
composer.phar create-project --prefer-dist yiisoft/yii2-app-advanced advanced
~~~  

这个参数 --prefer-dist 表示 强制使用压缩包，可能是源码太多，可能是镜像上也没有添加源码，而是只增加的压缩包。具体的原因不知道了，就是加上这个参数就可以下载很快。  
参考：https://segmentfault.com/a/1190000000355928  

### 4.配置好页面却无法访问。  
这个是个很冤枉的坑，眼看都下载了，配置好域名了，结果无法访问...  
解决：  
1. 是否初始化了？ 在命令行里执行 php init 选择0 development模式。  
2. 域名配置指向地址是否正确，一般是配置到web文件作为根目录。如果是advanced包，前台域名指向 /frontend/web/文件夹，后台域名指向/backend/web/文件夹。  
3. 都能访问了，需要配置好数据库，配置好之后需要在控制台，或者那个文件夹下执行迁移数据库命令： php yii migrate,数据库中就会自动生成两个表，一个migration,一个是user。  

到此，基本是把坑踩完，愉快的coding了~  
[ 刚学的框架，名称还没搞清楚来，还愉悦的coding,说这话时脸皮真够厚的来... ]  

### 曾经的热血青春  
<center><embed src="http://player.video.qiyi.com/b9ceb85b97b4423468dbf1debc752152/0/0/w_19rtxq9qbp.swf-albumId=7740824809-tvId=7740824809-isPurchase=0-cnId=5" allowFullScreen="true" quality="high" width="480" height="350" align="middle" allowScriptAccess="always" type="application/x-shockwave-flash"></embed></center>

