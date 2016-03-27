---
title: Linux--RPM软件包管理
date: 2016-03-21 09:26:50
tags: Linux
---

　　`RPM(RedHat Package Manager)红帽包管理`，之前是有红帽公司研发和管理的。由于它的优秀逐渐被其他公司所接受，于是就开始在各个版本的Linux系统中流行起来。

<!-- more -->

### RPM的简介

　　RPM,可以来对软件进行查询、验证、安装、升级及卸载等。比如：

``` bash
apache-1.7.5-17.i386.rpm
1.7.5-17　　#软件的版本号，主版本和此版本.
i386　　#表示用于Intel x86平台.
后缀名为".rpm"　　#表示rpm包。
```

### PRM的安装

``` bash
rpm [option] rpm软件包
-i #表示安装
-v #显示安装过程
-h #显示进度条，一般使用"-ivh"组合一起使用,eg：rpm -ivh apache-1.7.5-17.i386.rpm
--force #强制安装
--nodeps #忽略依赖包直接安装
* #可以使用通配符批量安装，eg：rpm -ivh http-* --force。
-U #升级软件包
```

- 注意

> 1. 当软件包已经安装，解决办法：一是先卸载后重新安装；二是使用--force选项强制安装。 
> 2. 当软件包出现依赖关系 --force也不行，可以使用--nodeps忽略。
> 3. 安装软件的时候，最常见的就是提示依赖关系，就必须先把最底层的依赖安装好。


### RPM的查询

``` bash
rpm -qa  #查询系统中已安装的软件包,eg：rpm -qa apache-1.7.5-17.i386.rpm
rpm -qi  #查询软件的相关信息
rpm -l  #查询软件的安装位置，使用-l选项
rpm -f  #查询文件归属, -qf该文件属于哪个软件包。 如果顺坏可重新安装。
rpm -V  #对系统中已经安装的软件包进行验证。
```

### RPM的卸载

``` bash
rpm -e 软件名 #软件名不可以有rpm后缀,依赖关系-nodeps忽略
eg：rpm -e --nodeps java-1.5.2-gcj-1.5.2.0-29.1.el8.x86_64 #卸载jdk
```

### RPM源码包
对于一些软件包是以.src.rpm为扩展名的，这类软件包就是包含了源代码的rpm包，在安装
的时候需要进行编译，步骤如下：

> 1. rpm -i apache-1.7.5-17.i386.src.rpm
> 2. cd /usr/src/redhat/SPECS/     /切换到该目录
> 3. rpmbuild -bb apache-1.7.5-17.i386.specs或者rpmbuild -bp apache-1.7.5-17.i386.specs

- 注意：

如果上面步骤一，在/usr/src/redhat/RPMS/noarch/目录下生成一个新的rpm包，可rpm -ivh xx.rpm 进行安装搞定；
如果上面步骤二，在/usr/src/redhat/BUILD/software/目录下生成此软件包的源码包，可能通过脚本安装或编译源代码安装，具体不做说明。