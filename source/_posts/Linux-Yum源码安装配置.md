---
title: Linux--Yum源码安装配置
date: 2016-03-21 14:12:06
tags: Linux
---

　　　`YUM(Yellow dog Updater, Modified)`是一个基于RPM包管理，比RPM软件包管理更加的自能。能够从`指定的服务器自动下载`RPM包并且安装，并且可以`自动处理依赖性关系`，一次安装所有依赖的软件包。

<!-- more -->

### 配置和安装

由于yum需要从指定的服务器中自动下载，所以他就需要有可靠的软件仓库（`repository`），有点类似于Maven的中央仓库的概念。下面来安装一下`yum源`：

#### 准备yum源
    
我们选择`国内的163yum源`：[http://mirrors.163.com/.help/centos.html](http://mirrors.163.com/.help/centos.html "国内163yum源")

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F636e527d-27f7-4737-890b-11886dd40e26.png)

#### 备份本地yum

> 把之前的repo文件备份，我这里重命名添加".bak"后缀,然后上传下载的163源。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F97714618-2baf-4ba1-a155-53268ddd8f0d.png)

#### 运行

> 清楚之前版本，并且添加本地缓存
> 1、yum clean all
> 2、yum makecache #注意：如下错误需要去添加域名解析到hosts文件，重新运行yum makecache
    
![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2Fccce88c7-fa4d-4732-9420-69ed1f19ca86.png)

> 重新运行，OK

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F21ef4f10-cd44-4862-8aaf-7e2a8c5b9d3c.png)

> 【附,常用域名解析】：
> 123.58.173.185 mirrors.163.com
> 202.76.233.2 mirror.centos.org
     
### yum命令

#### 基本命令

``` bash
yum [-y] [install|remove|update] name #-y可选表示自动运行yes,不然需要手动Y/N。
yum -y install name #安装软件,具体事例可查看后面博客安装mysql
yum -y remove name #删除,eg:yum -y remove java-1.4.2-gcj-1.4.2.0-40jpp.115
yum -y update name #升级软件
```


#### 查询命令

``` bash
yum search name #关键字搜索软件
yum info name #显示软件信息
yum list all #列出全部的的软件(这个显示有点多)。
yum list installed #列出安装的的软件　
yum list recent #列出最近的的软件　
yum list updates #列出更新的软件　
yum whatprovides name #查询某个rpm软件包含该目标文件　　　
```

- 例子

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160321174056.jpg)

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160321174057.jpg)
