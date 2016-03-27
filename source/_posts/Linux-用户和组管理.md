---
title: Linux--用户和组管理
date: 2016-03-18 15:00:36
tags: Linux
---
　　在Linux系统中，用户信息及密码，组信息及其密码，都保存在不同的文件中，1.用户信息（`/etc/passwd`），2.用户密码（`/etc/shadow`），3.用户组帐号（`/etc/group`），4.用户组密码（`/etc/gshadow`）。用户和组是多对多的关系，即一个用户可以属于多个组，一个组也可以包含多个用户。

<!-- more -->

### 配置文件

#### **/etc/passwd**

保存则着所有用户信息，密码使用了x表示，

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160314155129.png)

分别表示：用户帐号 用户密码 用户ID 用户组ID 用户名全称 用户主目录 用户所使用的shell。
该文件默认就会初始化很多用，当shell等于/sbin/nologin时就表示该用户不能登陆。

#### **/etc/shadow**

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160314155130.png)

第二位为用户密码，使用了MD5加密算法。

#### **/etc/group**

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160314155131.png)

分别表示：用户组名称 x 用户组ID 用户组成员列表 

#### **/etc/gshadow**

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160314155132.png)

### 用户管理

- 添加用户

> useradd [option] userName
> -d dir ：#指定目录，默认目录/home/userName
> -n ： #不为用户创建私有用户组
> -g groupName : #指定用户组，该用户组必须存在,eg：useradd -g blogger xiaoxiaomo
> -G groupName1,groupName2 ： #指定多个组
> -p passWord ： #指定用户密码，eg：usreadd -p 123456 xiaoxiaomo


![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160314155133.png)

- 修改用户

> usermod [option] userName
> usermod -l newUserName userName #修改用户名。
> usermod -d 原目录 新目录名称 #修改用户目录，eg：usermod -d /home/xiaoxiaomo momo。
> usermod -L userName #锁定用户，锁定后用户密码前会有感叹号，解锁使用-U，可用-S查看状态。


- 设置密码

> passwd [userName] #带参数修改某用户密码（一般root用户才有权限），不带参数修改自己的密码。
> passwd -l userName #锁定用户密码，解锁使用-u。
> passwd -d userName #删除用户密码。

- 删除用户

> userdel userName   #删除用户保留文件夹
> userdel - userName #删除用户不保留文件夹

### 用户组管理

- 添加组

> groupadd [-r] groupName #创建用户组，带-r,会创建系统组GID<500,不带-r,GID>=500。
> groupmod -n newGroupName groupName #修改组名称。
> groupmod -g newGroupId groupId #修改组GID，不可与已有Id重复。

- 删除组

> groupdel groupName #注：删除组是应先删除用户，被删除的组不能是某个账户的私有用户组。

- 用户和组

> gpasswd -a userName groupName #添加用户到某个组（root用户和改组管理员又该权限）。
> gpasswd -d userName groupName #把某个用户从组中删除（root用户和改组管理员又该权限）。
> gpasswd -A userName groupName #设置userName为组管理员。
> groups userName #查看用户所属组

### 权限管理

#### 授权

```
chmod [option] 文件或目录
```

> chmod 777 文件目录 #授权rwxrwxrwx。
> chmod u=rwx,g=rwx,o=rwx #等同上面的授权。
> chmod o-x,g+w 文件 #文件去除其他组用户执行的权限，增加组写的权限。
> chmod a+w  #给所有用户添加自读权限。

#### 修改所属

改变文件/目录所属者

```
chown xiaoxiaomo 文件/目录  #改变文件/目录的所有者为xiaoxiaomo
chown ‐R root 文件/目录  #改变文件/目录以及子目录文件的所有者为root
```

改变文件/目录所属者

```
chgrp root 文件/目录：改变文件/目录所属的组为root
```
