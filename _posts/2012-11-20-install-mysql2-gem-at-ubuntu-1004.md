---
layout: post
title: "ubuntu10.04下安装mysql2失败的解决方法"
summary: "如何在ubunt下面安装mysql2的gem,以及出错的解决方法"
category: 
tags: [mysql, ubuntu, rails]
---
{% include JB/setup %}

首先执行：gem install mysql2 出错，错误信息如下：
{% highlight c %}
ERROR:  Error installing mysql2-0.3.10.gem:
ERROR: Failed to build gem native extension.
 
/home/liuqi/.rvm/rubies/ruby-1.9.2-head/bin/ruby extconf.rb
checking for rb_thread_blocking_region()... yes
checking for rb_wait_for_single_fd()... no
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lm... yes
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lz... yes
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lsocket... no
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lnsl... yes
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lmygcc... no
checking for mysql_query() in -lmysqlclient... no
*** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of
necessary libraries and/or headers.  Check the mkmf.log file for more
details.  You may need configuration options.
 
Provided configuration options:
--with-opt-dir
--without-opt-dir
--with-opt-include
--without-opt-include=${opt-dir}/include
--with-opt-lib
--without-opt-lib=${opt-dir}/lib
--with-make-prog
--without-make-prog
--srcdir=.
--curdir
--ruby=/home/liuqi/.rvm/rubies/ruby-1.9.2-head/bin/ruby
--with-mysql-config
--without-mysql-config
 
Gem files will remain installed in /home/liuqi/.rvm/gems/ruby-1.9.2-head@rails310/gems/mysql2-0.3.10 for inspection.
Results logged to /home/liuqi/.rvm/gems/ruby-1.9.2-head@rails310/gems/mysql2-0.3.10/ext/mysql2/gem_make.out

{% endhighlight %}

解决方案如下：   

`sudo apt-get install libmysql-ruby libmysqlclient-dev`   

可是在安装libmysqlclient-dev的过程中又出现错误：   
下列软件包有未满足的依赖关系：
libmysqlclient-dev: 依赖: libmysqlclient16 (= 5.1.41-3ubuntu12.7) 但是 5.1.41-3ubuntu12.10 正要被安装
E: 破损的软件包

由于我的ubuntu10.04的默认的libmysqlclient-dev版本是5.1.41-3ubuntu12.7，所以只能去下载一个12.10版本的手动安装一下，下载地址：   
[点这里下载](http://launchpadlibrarian.net/63912696/libmysqlclient-dev_5.1.41-3ubuntu12.10_i386.deb)

安装成功后，再次执行：

`sudo apt-get install libmysql-ruby libmysqlclient-dev`
     
`gem install mysql2`

###success！
