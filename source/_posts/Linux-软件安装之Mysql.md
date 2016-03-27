---
title: Linux--软件安装之Mysql
date: 2016-03-22 14:14:37
tags: [Linux,Mysql]
---

　　Mysql的安装，第一次自己去折腾的时候倒挺麻烦的，下载哪一个版本的mysql都不确定。之后在DBA的帮助下，很顺畅的就完成了，在这里呢总结一下安装流程：

<!-- more -->

### 准备

可以去官网下载mysql数据库，我这里下载的是：mysql-5.7.9-1.el6.x86_64.rpm-bundle.tar，[点击](http://yun.baidu.com/share/link?shareid=1740266037&uk=2971593620)这里可下载。

检测系统中是否存在mysql，存在就卸载

``` bash
命令：rpm -qa | grep mysql
通过rpm安装mysql
```

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F3d24438d-fb81-407c-8b7a-fc2beeabe541.png)

### 卸载Mysql

``` bash
【命令】：rpm -e mysql // 普通删除模式（如有依赖无法卸载）
【命令】：rpm -e --nodeps mysql // 强力删除模式（可以忽略依赖）
【命令】：yum -y remove mysql    // yum卸载可以卸载依赖包
```

如下信息，就需要--nodeps忽略依赖

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F6143abdf-ad73-4820-98f2-94e838002ef5.png)


### 安装Mysql


> 1. 上传我们下载好的mysql tar文件。
> 2. 然后使用命令：tar -xvf ；发现mysql包含了很多的rpm文件。
> 3. 我们需要使用`rpm命令`从上面的rpm文件一个一个的安装。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F3513692b-9334-48f9-af70-48954f0ffd44.png)

- 安装第一个mysql-community-common-5.7.9-1.el6.x86_64.rpm，第一个顺利完成。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2Fa9d79ab9-3113-446a-baec-22357343b1a6.png)

- 安装第二个mysql-community-server，发现需要依赖包mysql-community-client

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F93e5c0ff-bb41-4434-9924-c5895355deea.png)

- 于是我们安装mysql-community-client，发现需要依赖包lib，

![mysql-community-client](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2Fe2db2b30-08e2-4984-885d-79b5242fff45.png)

- 然后安装lib成功，安装client也成功了,目前到这里还是比较顺利。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F18932347-c250-49d0-8130-2825f1728e2b.png)


- 然后再次尝试安装server,发现还需要很多的依赖包。晕菜了，这么多，
- 这个可以按照上面的方法逐步安装,是可以得，博客中就不讲解了，换成使用yum命令。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2Fede8b13f-5c40-448c-a7f9-c118a6f65d29.png)

- 使用yum命令安装一下server，最下图表示安装完成！

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F3275131b-9925-4135-8a6b-afc2669f9537.png)

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160322231708.jpg)

### 初始化mysql


![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2Ff5507559-ea43-444b-b00a-653951f98d08.png)
mysql_install_db is deprecated. Please consider switching to mysqld --initialize，mysql_install_db已弃用，使用新命令。


- `mysqld --initialize`命令不现实任何信息，表示是个好的结果，去`var/log/mysqld.log`查看一下日志，这里面记录了mysql的初始密码

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F5776c6c1-3088-4228-9009-c85a555b0415.png)

- 尝试启动一下mysql

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F7bc033d1-cd37-49fa-8ba4-ec483e813db6.png)


- 启动失败，这时候需要去`/var/lib`修改一下mysql的所属权限

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F2243b2ad-c8e7-4bdf-9b34-70c32cf2549b.png)


- 重新启动mysql数据库，然后设置密码，就可以登陆了。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F5ce9ebab-82bb-4a6f-aa4b-8a1224e4e6a4.png)


   
















