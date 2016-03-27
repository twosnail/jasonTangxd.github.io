---
title: Linux--软件安装之Redis
date: 2016-03-23 09:16:23
tags: [Linux,Redis]
---

　　`Redis`是一个开源（BSD许可）的，`内存中的数据结构存储系统`，它`可以用作数据库、缓存和消息中间件`。 它支持多种类型的数据结构，事务等。

<!-- more -->

### 下载/安装

- 1、官网下载：

> [http://redis.io/download](http://redis.io/download)  #官方下载
> *wget http://download.redis.io/releases/redis-3.0.6.tar.gz* #命令下载：（比较慢）

- 2、解压编译源码安装

``` bash
tar -zxvf redis-3.0.6.tar.gz -C /usr/local/src　　　#解压缩到指定目录
cd /usr/local/redis-3.0.1/　　　#到解压的目录去编译源码
make PREFIX=/usr/local/redis install　　　#安装到指定目录
```

`注`：如果make失败，一般是你们系统中还未安装gcc,那么可以通过yum安装：`yum install gcc`


### 将redis做成服务

``` bash
####将redis_init_script复制到/etc/rc.d/init.d/同时改名为redis
cp /usr/local/src/redis-3.0.1/utils/redis_init_script /etc/rc.d/init.d/redis
vim /etc/rc.d/init.d/redis

####修改3个地方
> #chkconfig: 2345 80 90   ##这个在上面蓝色字体第二行
> EXEC=/usr/local/redis/bin/redis-server　　##第七行
> CLIEXEC=/usr/local/redis/bin/redis-cli　　##第八行
> $EXEC $CONF &　　　　##第二十行
```

`注`：后面的那个“&”，即是将服务转到后面运行的意思

修改后，文件如下

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F0f8d10bb-a736-49b6-9c3e-1201ca161082.png)

### 配置redis


``` bash
###配置文件拷贝到/etc/redis/${REDISPORT}.conf 
mkdir /etc/redis   
cp /usr/local/src/redis/redis.conf /etc/redis/6379.conf
###这样，redis服务脚本指定的CONF就存在了。
###默认情况下，Redis未启用认证，可以通过开启6379.conf的requirepass 指定一个验证密码。 
```

> 注册redis服务：

``` bash
chkconfig --add redis 
```

> 然后将Redis的命令所在目录添加到系统参数PATH中


``` bash
vi /etc/profile　　　　＃编辑环境变量
export PATH="$PATH:/usr/local/redis/bin"　＃添加环境变量（记得指定到自己的目录）
source  /etc/profile　　　#重启配置
```

redis安装就完成了！