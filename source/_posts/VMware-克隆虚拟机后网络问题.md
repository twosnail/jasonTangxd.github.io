---
title: VMware--克隆虚拟机后网络问题
date: 2016-03-15 20:44:35
tags: VMware
---


### 1. 【问题】 ###
	
> 使用VMware克隆功能后，会发现网卡有问题

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F9f23d0d7-d158-4302-b4f0-ed2f3a507edd.png)
	
### 2. 【解决】  ###

> 由于网络配置中的网卡MAC地址还是之前虚拟机的，需要去复制出该虚拟机新生成的MAC地址到网络配置中

<!-- more -->

- 具体步骤

> 需要去 **/etc/udev/rules.d/70-persistent-net.rules** 复制出eth1（一般是最后一个网卡信息）的MAC地址到 **/etc/sysconfig/network-script/eth0** 。
>  
> ①、修改eth0为：eth1（一般是最后一个）
> ②、修改HWADDR为：01:0c:29:43:21:3c（此网卡是作者电脑例子）
> ③、其中无用的eth0可以删除（保留最后一个就行）

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F06295951-0670-4a7a-b633-a9f35a0166c3.png)

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F8ab829c9-afb6-41a7-875d-5d3dae6bd05c.png)

### 3. 【使用】 ###
    
> 重启服务即可：service network restart

	

