---
layout: post
title: "ubuntu下定时备份mysql"
summary: "通过创建crontab任务来实现mysql的定时备份"
category: 
tags: [mysql, ubuntu, timed backup]
---
{% include JB/setup %}

###方案选择
当我们的应用开发告一段落，就需要部署在生产环境下对外公开了。这时候的数据安全性就会非常重要，除了做好硬件级别的，操作系统级别的，应用级别的各种安全防护措施之外，对数据的备份也是必不可少的。  
所以计划是每天把数据库备份一次，以备不时之需。定时备份的方案有多种选择，mysql自从5.1之后本身就支持定时任务，也可以利用linux本身的crontab定时任务来解决。我选择了第二种。

###生产环境
####os: ubuntu server 12.04  
####mysql:5.5

###操作步骤
####1 写定时备份的shell文件
{% highlight sql %}
time=`date +%Y%m%d` 
mysqldump wisdom_production -u root -pyourpassword > /home/wisdom/databackup/mysql/mysql$time.sql
{% endhighlight %} 
wisdom_production是数据库的名字，如果你想备份所有的数据呢，就改成--all-databases

####2 创建用来备份的数据库文件夹
mkdir /home/wisdom/mysqldata

####3 编辑crontab文件，把写好的shell文件去定时执行
sudo vi /etc/crontab  
在# m h dom mon dow user	command之后加上:  

`12 3    * * *   root    sh /home/wisdom/mysqltimer`   

意思就是每天3点12分去执行mysqltimer文件   
各个字段的具体含义是：分钟 小时 日期 月份 星期 命令，在某月（mon）的某天（dom）或者星期几（dow）的几点（h，24小时制）几分（m）执行某个命令（command），*表示任意时间。

除了vi /etc/crontab之外，你也可以使用crontab -e来编辑文件

####4 准时准点成功产生文件
successful!

####5 后续工作
后面还有很多工作需要完善，例如:   
数据库文件多了之后，还要再建立一个定时删除的任务.  
如果数据量很大，备份数据库之前是否需要把数据库进程先暂时停掉一段时间，以避免在备份过程中有数据进入.  
各种情况的处理方案，就留给各位一起探讨吧。