---
title:  "多个git账号的配置"
date:   2023-05-11 16:30:51 +0800
categories: 服务器
tags: 总结
author: PoplarY
description: 配置多个git相关信息
---

### 需求
同一台电脑使用自建的仓库平台，同时还需要使用其他仓库平台，需要不同的项目对应不同的平台情况
比如项目A需要gitee上仓库；项目B需要github上仓库

### 生成 ssh 密钥
linux系统
```
ssh-keygen -t ed25519 -C "Gitee User A" -f ~/.ssh/gitee_user_a_ed25519

ssh-keygen -t ed25519 -C "Github User B" -f ~/.ssh/github_user_b_ed25519
```
### 仓库平台添加密钥
```
cat ~/.ssh/gitee_user_a_ed25519.pub
复制数据，添加到gitee上
```
```
cat ~/.ssh/github_user_b_ed25519.pub
复制参数，添加到github上
```

### 修改 ssh 配置信息
创建或修改 ~/.ssh/config
```
Host gt_a
    User git
    Hostname gitee.com
    Port 22
    IdentityFile ~/.ssh/gitee_user_a_ed25519
Host gt_b
    User git
    Hostname github.com
    Port 22
    IdentityFile ~/.ssh/github_user_b_ed25519
```
### 验证
``` 
ssh -T gt_a
Hi Gitee User A! You've successfully authenticated, but GITEE.COM does not provide shell access.

ssh -T gt_b
Hi Gitee User B! You've successfully authenticated, but GITEE.COM does not provide shell access.
```
### 拉取代码
将 git@gitee.com 替换为 SSH 配置文件中对应的 Host，如原仓库 SSH 链接为：  
git@gitee.com:owner/repo.git  
使用帐号 A 推拉仓库时，需要将连接修改为：  
gt_a:owner/repo.git

### 参考信息
[码云-帮助手册](https://help.gitee.com/repository/ssh/how%20to%20configure%20multiple%20SSH-Keys)

### 后记
gitee服务器上建议使用 部署公钥 允许以只读的方式访问仓库