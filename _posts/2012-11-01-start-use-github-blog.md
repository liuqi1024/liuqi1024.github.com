---
layout: post
title: "追赶文艺范儿：使用jekyll + github写作"
summary: "不需要搭建独立的服务器空间，不需要学会配置LAMP环境，不担心写过的东西会丢失，不需要在写作的时候关心页面的排版和样式，只写出你想写出的内容，简约，清新，如果你需要这样的创作环境，那么开始使用jekyll并且把他发布在github上吧。"
category: jekyll
tags: [jekyll, github, blog]
---
{% include JB/setup %}
### 开始使用
不需要搭建独立的服务器空间，不需要学会配置LAMP环境，不担心写过的东西会丢失，不需要在写作的时候关心页面的排版和样式，只写出你想写出的内容，如果你需要这样的创作环境，那么开始使用jekyll并且把他发布在github上吧。   
简约，清新，这不正是追求的文艺范儿风格 ^_^

### 需要掌握的知识
这不是一篇step by step的教学文章，需要用到的各方面知识，可以在相关的官网上得到更加细致的说明。我在这里主要介绍一下我搭建的过程中的操作步骤以及遇到的问题和解决方案，希望能对大家也有所帮助。   

- **jekyll是什么**   
jekyll是一个简单的免费的Blog生成工具，类似WordPress。但是和WordPress又有很大的不同，原因是jekyll只是一个生成静态网页的工具，不需要数据库支持。

- **git & github**   
  git是一种分布式版本管理系统，可以查看专门的git书： [Pro Git](http://git-scm.com/book/zh),里面支持多语言版本，可惜被墙了。近些年git也是越来越流行，相关的资料很多，不难找到。   
  [gitHub](https://github.com/)是一个面向开源及私有软件项目的托管平台，因为只支持git作为唯一的版本库格式进行托管，故名gitHub。

- **github pages**   
github pages是github提供的托管服务，你可以把自己的主页或者blog托管在上面，和其他的主机托管服务不同的是，大多数托管平台无非是开放一个FTP或类似服务，用户把制作好的网页或脚本上传了事，而在gitHub用户可以对自己的blog进行版本管理，very cool！   
另外，如果有域名，还可以把域名指向你的blog，而且操作非常简单。

- **markdown又是什么**   
Markdown 是一种轻量级的标记语言,允许 HTML 语法，所以使用者如果需要可以直接用 HTML来表示是可以的，推荐一个快速入门的[教程]。(http://wowubuntu.com/markdown/basic.html)

- **如何把markdown转换为html页面呢？**   
这就是markdown的引擎要做的事情。jekyll默认引擎为maruku，可以替换成rdiscount。
	
### 操作步骤
1. **install jeklly**  
安装命令很简单:  
`gem install jekyll`   
具体的安装依赖和不同操作系统下的安装方式请参考官网：[jekyll install](https://github.com/mojombo/jekyll/wiki/Install)  

2. **jekyll bootstrap 快速搭建运行环境**  
官网首页的介绍和操作指引很详细，命令行都帮你自动生成了，[点击这里查看](http://jekyllbootstrap.com/)，前提你是你要有一个github的账号。   
照着步骤操作完成后，你就可以在本地启动一个jekyll的服务器，并且查看自己的运行结果页面了，同时也可以把新产生的页面发布到github上。   
jekyll bootstrap的document也写的很详细：[点击这里查看](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)。   
*创建一篇文章:*    
 `rake page name="about.md"`   
*安装主题:*   
`rake theme:install git="https://github.com/jekyllbootstrap/theme-the-program.git"`

3. **语法高亮？使用pygments吧**   
对于需要经常贴代码来说明问题的程序员来说，语法高亮的功能不能缺少，使用pygments来做jekyll的高亮显示吧，[jekyll wiki](https://github.com/mojombo/jekyll/wiki/Liquid-Extensions)里也有说明。   
*安装*:还在刚才的jekyll的安装wiki页面可以找到
{% highlight ruby %}
brew install python
# export PATH="/usr/local/share/python:${PATH}"
easy_install pip
pip install --upgrade distribute
pip install pygments
{% endhighlight %}   
*配置好_config.yml*: `pygments: true`   
*生成css文件，并且引入到你的layout页面里。*	
`pygmentize -S default -f html > css/pygments/default.css`   
default是指的默认的模版的名字，官网可以查看有多种模版可选择，后面的css指的你要产生文件的路径。

####**最后，如果有自己的域名，可以指向那里。**   
在本地代码库里新建名为CNAME的文本文件，把域名地址放进去。   
假设你的域名是[liu-qi.com](www.liu-qi.com)，可以用命令   
`echo 'liu-qi.com' > CNAME`   
接着在自己的域名注册商那里改一下指向。

### 资源推荐
在学习的过程中看到过好的wiki和一些写的很详细的文章，推荐出来，可以作为参考:   
- jekyll: 最全面的资料莫过于官网的 [Jekyll Wiki](https://github.com/mojombo/jekyll/wiki) 了,涵盖了几乎所有的知识点，包括安装的步骤。美中不足的就是英文读起来效率有点低。   
- [Jekyll建站之旅](http://calefy.org/2012/03/03/my-process-of-building-jekyll-blog.html)   
- [Markdown 语法说明](http://wowubuntu.com/markdown/index.html)   
- [用Jekyll构建静态网站](http://yanping.me/cn/blog/2011/12/15/building-static-sites-with-jekyll/)
