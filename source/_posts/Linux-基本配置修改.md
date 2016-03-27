---
title: Linux--基本配置修改
date: 2016-03-24 09:19:57
tags: Linux
---

　　本博客介绍一些我们常用linux配置文件的修改，主要包括网络地址，主机名，hosts文件，端口，防火墙等基本操作。

<!-- more -->

### 修改网卡

　　网络接口（网卡）的脚本文件`ifcfg-eth0`是默认的第一个网络接口，在`/ect/sysconfig/network-script/`目录下。如果有多个会以`ifcfg-ethn`命名n为（0，1，2，3，4......）

```
$ vim /ect/sysconfig/network-script/ifcfg-eth0
```

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160324093923.png)
参数说明：
``` bash
DEVICE　　#网卡名,在`/etc/udev/rules.d/70-persistent-net.rules`有中有记录。
HWADDR　　#MAC地址,和网卡相对应。
USERCTL　　#[yes|no]（非root用户是否可以控制该设备）
BOOTPROTO　　#IP的配置方法[none|static|bootp|dhcp]（|静态分配IP|BOOTP协议|DHCP协议）
ONBOOT　　#系统启动的时候网络接口是否有效（yes/no）   
TYPE　　#网络类型（通常是Ethemet）   
NETMASK　　#网络掩码   
IPADDR　　#IP地址   
IPV6INIT　　#IPV6是否有效[yes/no]   
GATEWAY　　#默认网关IP地址
BROADCAST　　#广播地址
NETWORK　　#网络地址
```


![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160324095902.png)

### 修改主机名

``` bash
$ vi /etc/sysconfig/network   #修改这个文件，系统生效
```

- 还有一种方法修改：hostname命令。（临时修改，机器重新启动之后就会恢复原来的值）

``` bash
$ hostname　　　　//查看机器名
$ hostname -i  //查看本机器名对应的ip地址
$ hostname 新名称　　//修改主机名(临时有效)
```

### 修改hosts文件
``` bash
$ vi /etc/hosts　　#修改ip和域名/主机名映射
```

例如：

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160324100025.png)

### 修改默认端口
    
1. 修改配置文件：/etc/ssh/sshd_config ，找到#port 22 ，如图
![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F75e6c306-ec03-4767-b39d-42139b2cf43e.png)

2. 先将Port 22 前面的 # 号去掉，并另起一行。如定义SSH端口号为21117，则输入（建议在万位的端口）
![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2Ffe475739-4f9b-461d-b08c-bc2c0c209444.png)

3. 修改完毕后，重启SSH服务，并退出当前连接的SSH端口![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2Fdca4f2c3-1d50-4162-ab37-90d482b725fc.png)

4. 退出后，重新连接一下，链接成功后可以删除22那行记录。


### 禁用root本地或远程登陆
1. 禁止root本地登录

> 修改/etc/pam.d/login文件增加下面一行
> auth required pam_succeed_if.so user != root quiet

2. 禁止root远程ssh登录

> 修改/etc/ssh/sshd_config文件，将PermitRootLogin yes 改为no

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F5e15de04-7cca-4ae3-b555-5325718f7063.png)

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2Fd66c86e2-53c1-424b-b884-5f2fc64be994.png)
3. 重新启动sshd服务。
    

### 关闭防火墙

``` bash
$ service iptables XX
$ service iptables status
$ service iptables stop
```

- 防火墙是否开机自启动

``` bash
$ chkconfig iptables --list
$ vi /etc/inittab
$ chkconfig iptables off
```