---
title: Hexo搭建个人Github Blog
tags: [tech]
---

### 前言

  好久没写过认真构思的文章， 想要记录一下遇到的问题居然都有点无从入手。第一篇，有点乱。
  
  本文主要介绍初次利用HEXO搭建个人github博客的流程，以及在github备份博客后的二次快速搭建。

### 背景

开始玩gitblog的时候参看网上众多教程部署好了自己的博客。大概是十月初的时候。
主要参照物是[涛哥的博客](http://todd2010.github.io/2016/05/18/005-Hexo-GitHub/#more)。涛哥的博客写的简明清晰，欢迎大家关注。


<!-- more -->

### 一、首次利用HEXO搭建blog

##### 1. 安装Hexo
Hexo安装之前需要电脑上已经安装Node。博主当前使用node版本为v6.10.3, 配套npm版本为3.10.10。
使用npm安装Hexo。

    $ npm install -g hexo-cli
##### 2. Hexo建站

    $ hexo init
注意， hexo init会初始化当前文件夹为hexo建站目录。可以用如下指令生成一个新的名为blogName的文件夹作为blog目录。

    $ hexo init blogName
#### 3.下载依赖。
    $ npm install
#### 4. 生成网站文件，启动服务。

    $ hexo generate
    $ hexo server
至此，本地可以通过http://localhost:4000/访问自动生成的博客。

#### 5. 部署到github

修改_config.yml文件。
###### 1)  url: http://yoursite.com 改成 url: http://ABC123.github.io
###### 2) 把最下面的部署内容修改成如下代码并保存退出。
    deploy:
        type: git
        repository: https://github.com/Todd2010/Todd2010.github.io.git  //此处改成您的GitHub仓库地址
        branch: master


安装部署插件。

    $ npm install hexo-deployer-git --save
    $ hexo clean
    $ hexo generate
    $ hexo deploy 

至此，可通过yourProjectName.github.io访问博客。Hexo搭建个人博客已经完成。

### 二、备份博客到github
Hexo部署在ccflower.github.io项目中，是已经编译过的项目文件。而博客的源文件，包括文档，图片，配置，甚至主题，需要自己新建项目备份。博主折腾过在同一个项目中通过不同的分支来管理源文件和部署文件，后来觉得有点混乱，目前也采取额外新建一个项目[blogBackup](https://github.com/ccflower/blogBackup)存放博客源文件。

### 三、主题配置

目前博主采用[litten](litten.me)开发的[yilia](https://github.com/litten/hexo-theme-yilia)主题。具体主题如何配置改动后面再陆续补充。

### 四、配置个人域名

对大部分人来说，ccflower.github.io这样一个域名指向自己的博客地址已经足够用了。博主因为不了解域名的配置，花4RMB买了一个[ccflower.space](ccflower.space)的域名指向自己github的博客。时间久了具体步骤已经有点忘记了。下次重新折腾记得来补充。
### 五、利用blogBackup备份进行快速二次搭建

如果换电脑，或者不小心搞残了自己本地的博客配置，这个步骤将十分有用。

#### 1. 远程克隆项目

    git clone https://github.com/ccflower/blogBackup.git
克隆完成后，将.git文件拷贝出来备份。后续hexo init步骤会删除这个文件，还不理解原因。

#### 2. 进入项目，安装hexo

    npm install hexo --save
#### 3. 项目hexo初始化,安装依赖

    hexo init
    npm install
#### 4.启动hexo server，本地测试

    hexo s
#### 5.修改主题
拷贝_config.yml和themes文件夹，本地测试主题适用。

#### 6.将.git文件夹复制回blogBackup
#### 7.安装Hexo部署插件

    npm install hexo-deployer-git --save
#### 8.重新部署blog

    hexo clean  
    hexo g
    hexo d
#### 9. 将改动提交到blogBackup
    git status
    git add 
    git commit -m "..."
    git push

### 六、小结
使用Hexo搭建blog已经有一年多的时间，反复折腾过不少次。
踏过的坑，都是未来的经验。耐心总结梳理，对自己总会有所帮助吧。