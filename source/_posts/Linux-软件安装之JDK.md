---
title: Linux--软件安装之JDK
date: 2016-03-22 09:39:25
tags: [Linux,Java]
---

　　JDK（`jre+开发工具包`），即JDK包含了jre（`java虚拟机+核心类库`），jre主要是用来运行程序的，而jdk可以运行程序又可以用来开发。作为一个后端程序员，或者说使用一个运行在JVM虚拟机之上的语言和环境，对于jdk的安装是不可避免的，虽然比较简单，但也不要去忽略它。

<!-- more -->

### 移除自带虚拟机

``` bash
1. java -version #检查是否已经安装jdk(Ubuntu自带openjdk)。
2. rpm -qa|grep gcj #查看具体的信息,主要获取具体名称和版本，提供给卸载使用。
3. rpm -e --nodeps java-xxxx.x86_64 #卸载jdk。
```

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160321174156.png)

### 下载安装

我们这里使用tar.gz和rpm两种安装方式，选择一种即可，推荐使用tar.gz方式。下载后上传：

> rpm　下载地址：[jdk-7u67-linux-x64.rpm](http://pan.baidu.com/s/1eRoWe90 "rpm_jdk1.7_64位")
> tar.gz下载地址：[jdk-7u67-linux-x64.tar.gz](http://pan.baidu.com/s/1o7fSmLk "tar.gz_64位_jdk1.7")


#### rpm安装

rpm安装，下载上传相应的rpm文件，然后执行安装命令：

``` bash
rpm -ivh jdk-7u67-linux-x64.rpm #安装jdk,默认安装目录为/usr/java
```

#### tar.gz安装

[解压缩.tar.gz](http://blog.xiaoxiaomo.com/2016/03/17/Linux-%E5%8E%8B%E7%BC%A9%E5%8F%8A%E5%BD%92%E6%A1%A3 "Linux--压缩及归档"),把解压后的文件夹推荐放到/usr/local下面。（当然任意目录下都可以）：

``` bash
tar -zxvf jdk-7u67-linux-x64.tar.gz #解压jdk，会在当前目录下（自己改名或移动）
```

### 配置环境

- 第一种： 修改`/etc/profile`文件(开发环境推荐)

很方便所有用户都能使用，但存在一定安全性。 

> /etc/profile #在profile文件末尾添加如下配置，[具体修改操作](http://blog.xiaoxiaomo.com/2016/03/18/Linux-%E5%B8%B8%E7%94%A8VI-VIM%E5%91%BD%E4%BB%A4 "Linux--常见VI/VIM命令")：

``` bash
export JAVA_HOME=/usr/local/jdk1.7
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```

【注意】：

> 1. 你要将 /usr/local/jdk1.7改为你的jdk安装目录 
> 2. linux下用冒号“:”来分隔路径 
> 3. 等号左右不能有空格。
> 4. CLASSPATH中当前目录“.”不能丢

- 第二种： 修改`个人主目录/.bash_profile`文件（生产环境推荐）

这种方法更为安全，个人主目录配置了的用户才能使用
添加如上配置即可（略）。

- 第三种： 直接在`shell下设置变量`（不推荐，适合临时使用）

只对该shell有效。只需在shell终端执行如上命令即可（略）。

### 重新加载

重新加载配置，使用source命令

``` bash
source profile
```

### 测试

``` bash
java -version #或下面命令
javac -version #显示版本信息。
```
