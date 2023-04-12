---
layout: post
title:  "开发网站的一点入门总结"
date:   2017-10-12 14:10:51 +0800
categories: 非技术
tags: 总结
author: 葩木乐
description: 一些关于开发网站入门环境的总结
---

> 一个站点的开始到上线是个漫长的过程，从最初的规划到用户最后访问中间需要经过很多的步骤，
根据站点的简繁会有不同的流程，不同的攻城狮有不同的看法，这里只是根据自己工作以来的经验，
对这些信息做些简单的总结。有不恰当地方欢迎指出。

### 本地测试环境的搭建
#### phpstudy  
1. 程序放置目录： phpstudy/www/   (或其他固定的文件夹）
2. 添加本地访问域名，打开phpstudy控制面板  

> 1. 域名规则：客户要使用的域名加你的姓名简拼，（我的是ywf,若是张三可以是zs,注意，加这个目的是区分实际站点和本地站点，如果也使用com或cn或net等容易混淆网络和本地）如 taobao.com ,你的域名是 taobao.com.ywf  
> 2. 其他选项菜单 - 打开host - 编辑host : 最后一行添加" 127.0.0.1   taobao.com.ywf "(没有上下引号), 保存。
> 3. 其他选项菜单（或mysql管理器） - 站点域名管理：添加 taobao.com.ywf  指定文件夹位置，添加，保存并生成配置文件，重启Apache  
> 4. 前台浏览器访问 taobao.com.ywf  

#### IDE
集成开发环境（IDE，Integrated Development Environment ）是用于提供程序开发环境的应用程序。 
根据相关开发使用合适的编辑器。
php 推荐phpstorm。  

#### 版本控制  git  
外网版本库推荐开源中国的码云 http://gitee.com。  
如果自己搭建的话有开源的 gitlab 
> 参考文档：  
> 码云使用手册 http://git.mydoc.io/  
> 廖雪峰老师git学习文档  https://www.kancloud.cn/wizardforcel/liaoxuefeng/108732  
> https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000  
> 快速查阅  https://www.kancloud.cn/thinkphp/git-cheat-sheet  
> git学习资料集锦  http://www.jianshu.com/p/c8cf9a9b0270  
> git学习过关游戏，游戏中学习 https://learngitbranching.js.org/  

文件夹层次：  
/               ----根目录  
/www            ----程序存放目录。前台访问的程序  
/doc            ----相关文档,数据文件等  
/readme.md      ----说明  
/.gitignore     ----忽略文档  