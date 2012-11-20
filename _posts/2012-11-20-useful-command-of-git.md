---
layout: post
title: "git常用命令和操作"
summary: "列出了git常用的命令和操作，偶尔忘了的话可以来查一查"
category: 
tags: [git]
---
{% include JB/setup %}

###基本配置
在此之前先推荐一篇blog，[git简易指南](http://rogerdudler.github.com/git-guide/index.zh.html)，写的很通俗易懂，网页排版也很清新。想学习git的各位可以花半个小时在github上创建个账号，建立个repository。再花一两个小时把命令都执行一遍，就到入门级别了。   
[点击这里阅读](http://rogerdudler.github.com/git-guide/index.zh.html)   

**配置用户信息：**   
`$ git config --global user.name "John Doe"`   

`$ git config --global user.email johndoe@example.com`   

如果这样设置的话，文件在这个下面：   
cat ~/.gitconfig   
还有其他的配置方法，比如如果把global改为system，文件就存在于/etc下面了  

**创建别名：**
     $ git config --global alias.co checkout
     $ git config --global alias.br branch
     $ git config --global alias.ci commit
     $ git config --global alias.st status
**彩色的 git 输出：** `git config color.ui true`   

要检查已有的配置信息，可以使用 `git config --list` 命令

**内建的图形化git:** `gitk`

###关于分支
`git checkout -b yourbranch` **创建并切换到一个分支**

`git branch -d your branch` **删除本地分支**

`git merge yourbranch` **合并yourbranch分支到你的当前分支**

`git pull = git fetch + git merge yourbranch`

`git checkout --filename` **此命令是用HEAD中的最新内容，替换你工作目录的内容。已添加到缓存区的改动以及新文件都不受影响。
假如你想要丢弃你所有的本地改动与提交，可以到服务器上获取最新的版本并将你本地主分支指向到它：**

`git fetch origin`

`git reset --hard origin/master`


`git mergetool` 冲突解决工具

`git reset --hard` 取消冲突的合并让本地版本库回到合并之前的状态

在解决了所有文件里的所有冲突后，运行 `git add` 将把它们标记为已解决状态（实际上就是来一次快照保存到暂存区域。）


###关于github：
[GotGitHub](http://www.worldhello.net/gotgithub/index.html)这本教程写的很好，中文来介绍github的资料不多，推荐阅读。[点击这里阅读](http://www.worldhello.net/gotgithub/index.html)

`$ ssh-keygen` 

会产生一个公钥/私钥对，带.pub后缀名的是公钥，可以公开。没有后缀名的是私钥，需要保护起来。
需要把产生的公钥信息粘贴在github上的ssh public keys上面。一个github账号可以有多个公钥。

`ssh -T git@github.com`   
Hi liuqi1024! You've successfully authenticated, but GitHub does not provide shell access.

####个人主页和项目主页的区别？   

个人主页是建立一个跟你的github账号同名的repository，master分支。项目主页是为你账号下的每一个repository建立一个主页，必须要建立为gh-pages分支。   
建立个人主页和项目主页方法，一种是用命令行，上面推荐的GotGitHub都有讲到，还有一种更简单直接的方式是在github网站里通过界面去创建。

###关于rebase
有的资料翻译为变基，有的资料翻译为衍合，rebase的作用就是让分支看起来没有经过任何操作一样.操作命令如下:   
获取远程版本库的提交到本地的远程分支。   
`incredible$ git fetch origin`

执行变基操作，将本地master分支的提交变基到新的远程分支中。
`incredible$ git rebase origin/master`

如果一切顺利，变基后推送到共享版本库。    
`incredible$ git push`

**注意：一旦分支中的提交对象发布到公共仓库，就千万不要对该分支进行衍合操作**

[rebase更多操作点我查看](http://www.worldhello.net/gotgithub/04-work-with-others/020-shared-repo.html)




