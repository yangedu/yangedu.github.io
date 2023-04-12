---
layout: post
title:  "简述phpcms建站过程"
date:   2017-10-13 10:14:00 +0800
categories: php
tags: 总结
author: 葩木乐
description: phpcms是优秀的框架系统，使用该系统可快速的创建站点，很方便的，这里简要介绍下建站过程
---

首先，站点需要服务器和域名这两样东西，服务器就像买的房子，域名就是房子的门牌号，
用户要访问站点，就必须知道知道你的门牌号，按门牌号找你的房子时，还得必须存在那个房子。  
门牌号指向那个房子，房子承认这个门牌号是指的这个房子，否则的话就难访问到你的网站了。  

服务器和域名的购买请谷歌百度。  
域名指向服务器，服务器解析域名的方法，同样请谷歌百度。  

### 望-大体了解下站点都包含啥内容及模型

#### 站点的栏目类型
1. 单页  
这个打开就是一个页面，像关于我们，联系我们，大事件等基本是属于单页类型的，不排除特殊情况，自己定制其他类型的，如‘关于我们’可以是文章页，
里面包含更多的文章。  

2. 文章页  
这个就是文章的合集，数据返回的信息是多篇文章列表，有分页。  
这里注意下分级栏目情况，一级栏目有下级栏目，就不会存在分页的。

3. 详情页  
文章具体的内容页面。

#### 其他的模块  
1. 友情链接  
2. 表单(提交访客信息途径)  
3. 广告位 
4. 其他  

### 闻-创建phpcms原始站点

#### 本地测试域名及空间  
参考上篇文章 [开发网站的一点入门总结](http://somanywf.gitee.io/%E9%9D%9E%E6%8A%80%E6%9C%AF/2017/10/12/web-building-abc.html)  

#### 安装phpcms  
略

### 问-前台对phpcms动手  
1. 修改网站名称，在 后台-设置-站点管理 处修改  
2. 根据静态页区分单页和文章页，在 后台-内容-管理栏目 中添加相应的栏目。  
3. 根据静态页划分出部分推荐位，把推荐位名称修改恰当，到时候做模板时可方便点（如果模板多或没规划好，做的时候边做边改也是可行的）。  
4. 对应栏目添加些样例文章，请添加的标题和内容尽量符合本站的内容，尽量不要键盘上乱敲的标题和内容。如果时间紧张可以略过刚才前面说的要求。

### 切-给phpcms添加新模板  
#### 文件夹层级结构  
| 文件夹位置     | 说明 |  
| :----------   | :-----: |  
| /             | 根目录   |  
| /statics/     | 资源文件目录 |  
| /phpcms/template/ | 模板文件目录 |  
新加模板的话在 /phpcms/template/ 里新建文件夹即可，这里以mytest做例子。
#### 模板配置文件及新模板  
复制 /phpcms/template/default/config.php文件到/phpcms/template/mytest/config.php  
修改里面对应的文件夹名称。  
> name:模板名称  
author: 模板作者  
dirname: mytest 我的模板文件夹名  
homepage: 我的推广地址，个人站点  
version: 版本号  
其他的把default文件夹改成mytest即可  

模板这块参考他们的默认模板进行修改即可。  
模板语法文档：[phpcms帮助中心](http://v9.help.phpcms.cn/)  
1. 推荐位类型：position -相当于聚合文章，不局限于某个栏目的文章，是根据文章的推荐类型来展示的。
2. 列表类型: list  指定栏目的文章按顺序逐条显示。  
3. 栏目列表: category
4. 排行文章: hits
5. 内容相关文章: relation  
**以上均是内容模块**  
6. 友情链接: 友情链接模块 type_list  
7. 广告位: js调用
#### 常用模板文件  
content/index.html 首页  
content/category.html 栏目页（有下级)  
content/list.html 末级栏目页（最终文章列表)  
content/show.html 文章详情页  
content/page.html 单页（类似详情页)  
content/header.html 通用头部部分  
content/footer.html 通用尾部部分  
search/index.html 搜索页主页  
search/list.html 搜索结果列表页  
其他的通用部分可以根据项目的实际情况增加。  
新增页面也根据相同类型的文件名加下划线和新名称命名，如新加了一级栏目页可以是category_mytest.html，终级列表页 list_mytest.html这种。 

#### 模板资源文件  
文件夹 /statics/css/mytest/ 存放css文件
文件夹 /statics/js/mytest/ 存放js文件
文件夹 /statics/images/mytest/ 存放图片文件

模板文件中调用相关的css,js，图片时修改为  {CSS_PATH}mytest/a.jpg,其他的同理。  
{JS_PATH}  js的设置路径  
{IMG_PATH} 图片的设置路径
其中这些路径可以通过 后台-设置-基本设置中修改基础路径，  
也可以修改配置文件 /caches/configs/system.php中相关配置。