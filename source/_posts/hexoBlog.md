---
title: Hexo部署博客及采用git branch管理源文件
---

### 前言

  好久没写过认真构思的文章， 想要记录一下遇到的问题居然都有点无从入手。第一篇，有点乱。

### 背景

开始玩gitblog的时候参看网上众多教程部署好了自己的博客。大概是十月初的时候。
主要参照物是涛哥的博客啦（http://todd2010.github.io/2016/05/18/005-Hexo-GitHub/#more）。


后来适逢我厂大规模换电脑。而那时候只觉得我的博客已经部署到Git上了，
愉快地删除了所有的源文件。

然后领到新电脑，等再有时间来重新整理Hexo的时候，
又按照之前的步骤配置了一遍，等hexo deploy顺利执行完，刚准备舒口气，
刷新网页一看所有之前的内容都没有了（虽然本来就没啥）。


如果不想开两个项目来管理一个博客，只有借助分支来管理源文件和部署的静态文件了。搜到了CrazyMilk的博客（http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/#more）。


这篇文章对我很有启发。但是按照博主的步骤没有配置成功。原因在于每当执行hexo init后，clone的仓库的git的信息就丢失了。即使重新git init,并与远程仓库建立联系也遇到了很多问题。


所以最后只好反其道行之，在Hexo部署都设置好之后，重新初始化git仓库。建立远程连接。设置默认分支Hexo。在Hexo分支上提交src文件。在master
分支上部署静态文件。具体步骤如下。

#### 1. 安装Hexo
Hexo安装之前需要电脑上已经安装Node。
使用npm安装Hexo。

    $ npm install -g hexo-cli

#### 2. Hexo建站

    $ hexo init

注意， hexo init会初始化当前文件夹为hexo建站目录。可以用

    $ hexo init blogName
生成一个新的名为blogName的文件夹作为blog目录。


下载依赖。


    $ npm install
生成网站文件，启动服务。

    $ hexo generate
    $ hexo server
至此，本地可以通过http://localhost:4000/访问自动生成的博客。

#### 3. 部署到github

修改_config.yml文件。
安装部署插件。

    $ npm install hexo-deployer-git --save
    $ hexo clean
    $ hexo generate
    $ hexo deploy 

至此，可通过yourProjectName.github.io访问博客。

#### 4. 新建Hexo分支，存储源文件

初始化当前项目为一个git仓库。

    $ git init

与远程仓库建立联系

    $ git remote add origin https://github.com/ccflower/ccflower.github.io.git

获取远程仓库的最新状态

    $ git pull

创建新分支Hexo并切换

    $ git checkout -b Hexo

将新分支推送到远程。

    $ git push origin Hexo

在gitHub主页选择Hexo为默认分支。因为源文件的提交需要手动管理。master分之下只需要通过Hexo部署静态文件即可。

在Hexo分支下执行一下指令，将源文件提交到Hexo分支。

    $ git pull
    $ git status
    $ git add ******
    $ git commit -m "Here is comments."
    $ git push origin Hexo

需要重新部署博客时，只需要在Hexo分支下执行

    $ hexo clean
    $ hexo g
    $ hexo d
通过以上步骤，即可以利用master分支管理部署博客的静态资源。利用Hexo分支来更新源文件啦。其实只有Hexo分支需要手动管理。msater分支只是记录了Hexo的操作而已。So easy！
不过身边有个大神不喜欢非要部署，自己写了一个工具做静态发布。有时间再研究一下。

好啦，下次换电脑的时候，只需要clone下自己github.io的项目来，
在Hexo分支上就可以拿到所有的源文件啦。
然后安装Hexo， 安装依赖，安装部署插件，就可以继续发布新博客啦！
妈妈再也不用担心你的博客都被一键清理咯~~~~~~！


### 后续
后来觉得， 既然这是两个永远不需要merge的分支。干脆还是分开两个项目管理好了。所以下午打算重新来一遍啦~~~！

