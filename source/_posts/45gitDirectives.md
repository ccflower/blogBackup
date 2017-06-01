---
title: 常用Git指令
tags: [tech]
---


## 前言

十八摸代码管理工具使用的是内部产品RTC（Rational Team Concert）。同时也有自己的gitlab仓库。我们项目某一套组件依赖源码是通过git进行管理的。同时个人开发中也是git使用较多。

## git，github与gitlab

git是一个分布式版本控制系统。
跟早期的SVN，CVS等集中式版本控制系统相比，分布式版本系统将整个仓库下载到客户端，每个客户端作为一个独立的仓库运行工作。

github与gitlab是在线的基于Git的代码托管服务。便于团队存储，分享，发布，测试。

<!-- more -->

github免费账户只能创建公开代码仓库。是目前最火的开源社区平台。

gitlab可以创建免费的私人账户。同时可以设置不同的分组，用户权限等。

## 在Mac OS X上安装Git

直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。

## 设置committer
    $ git config --global user.name "Your Name"
    $ git config --global user.email "email@example.com"
## 基本指令

### 创建版本库
    $ git init
### 创建SSH Key
    $ ssh-keygen -t rsa -C "youremail@example.com"
### 克隆远程仓库
    $ git clone [repository url]
### 本地与远程仓库关联
    $ git remote add origin [git@github.com:ccflower/cotton.git]
### 添加文件 提交到远程
    $ git add [fileName]
    $ git commit -m "commit descritption"
    $ git push origin master
### 查看当前状态
    $ git status
### 查看修改内容
    $ git diff [fileName]
### 查看commit log
    $ git log
    $ git log --pretty=oneline --abbrev-commit
### 查看命令历史
    $ git reflog
### 恢复到某个版本
    $ git reset --hard [commit_id]
### 恢复到上个版本（适用于git commit 之后的文件）
    $ git reset --hard HEAD^
### 查看工作区和最新版本区别
注意：HEAD为本地版本库最新版本。

    $ git diff HEAD -- [fileName]
### 丢弃工作区修改（适用于git add 之前的文件）
    $ git checkout -- [fileName]
### 撤销暂存区修改，放回工作区（适用于git add 之后的文件）
    $ git reset HEAD [fileName]

理解工作区，暂存区和本地仓库的关系
![alt text](/assets/blogImg/45/1.jpg "理解工作区，暂存区和本地仓库的关系")

### 删除文件
    $ git rm [fileName]
## 分支

## 标签
### 创建标签
    $ git tag [tagName] [commitID]
### 查看所有标签
    $ git tag
### 指定标签信息
    $ git tag -a <tagname> -m "blablabla..."
### 用PGP签名标签
    $ git tag -s <tagname> -m "blablabla..."
### 删除标签
    $ git tag -d v0.1
### 推送标签到远程
    $ git push origin <tagname>
### 推送所有标签到远程
    $ git push origin --tags
### 删除远程标签
    $ git push origin :refs/tags/[tagName]

## 其它
在GitHub上，可以任意Fork开源仓库；
自己拥有Fork后的仓库的读写权限；
可以推送pull request给官方仓库来贡献代码。

理解fork项目和源项目

![alt text](/assets/blogImg/45/2.jpg "理解fork项目和源项目")

`.gitignore`文件可以设置git忽略的文件。

`.git/config`文件可以配置别名等。

    $ cat .git/config 
    [core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
        ignorecase = true
        precomposeunicode = true
    [remote "origin"]
        url = git@github.com:michaelliao/learngit.git
        fetch = +refs/heads/*:refs/remotes/origin/*
    [branch "master"]
        remote = origin
        merge = refs/heads/master
    [alias]
        last = log -1







参考文档：
SVN到RTC： http://www.uml.org.cn/pzgl/201204122.asp
Git，Gitlab和Github： http://blog.csdn.net/carryoner/article/details/51684431
                                     http://blog.csdn.net/ylgwhyh/article/details/52134338
Git常用指令教程：http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

