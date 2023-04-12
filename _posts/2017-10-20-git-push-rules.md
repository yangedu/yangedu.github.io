---
layout: post
title:  "提交git备注信息的规则[转]"
date:   2017-10-20 9:10:51 +0800
categories: git
tags: 总结
author: 葩木乐
description: 提交git信息时，填写的一些备注信息
---
## git提交代码时备注格式
每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。
~~~
<type>(<scope>): <subject>// 空一行<body>// 空一行<footer>
示例：
fix(m_user controller order action):修复数据库错误和字段错误
feat(m_common controller stadium action):添加会员场馆列表
fix(order model):修复订单模型变量错误
style(header):修改通用头部样式
~~~
其中，Header 是必需的，Body 和 Footer 可以省略。
不管是哪一个部分，任何一行都不得超过72个字符（或100个字符）。这是为了避免自动换行影响美观。
### type项
~~~
type用于说明 commit 的类别，只允许使用下面7个标识。
feat：新功能（feature）
fix：修补bug
docs：文档（documentation）
style： 格式（不影响代码运行的变动）
refactor：重构（即不是新增功能，也不是修改bug的代码变动）
test：增加测试
chore：构建过程或辅助工具的变动
如果type为feat和fix，则该 commit 将肯定出现在 Change log 之中。
其他情况（docs、chore、style、refactor、test）由你决定，
要不要放入 Change log，建议是不要。
~~~
### scope项
scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。
### subject项
subject是 commit 目的的简短描述，不超过50个字符。
以动词开头，使用第一人称现在时，比如change，而不是changed或changes
第一个字母小写
结尾不加句号（.） 
 
> PS:  
可以参考一些大公司的软件更新日志，比如QQ，小米UI，各种游戏的更新说明等等