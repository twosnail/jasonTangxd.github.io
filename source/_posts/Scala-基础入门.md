---
title: Scala--基础入门
date: 2016-03-25 18:34:53
tags: Scala
---

　　最近在看`Scala`，可能刚学不久的原因不是很习惯它的语法，总感觉怪怪的。自己也感觉一直飘着似的，所以想用写博客的形式来加深一下记忆，和大家一起学习。

<!-- more -->

## 简介/安装

Scala，是一门运行在JVM上的函数式面向对象语言，可以很好的兼容java。

> 1、首先安装一下JDK(略)
> 2、安装scala，官方下载：[http://www.scala-lang.org/download/2.11.0.html](http://www.scala-lang.org/download/2.11.0.html)；
> 3、配置好环境变量（略）

配置好后，打开cmd命令窗口，输入scala就进入了友好的scala的"`Repl`"界面，如图：

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325190300.png)

在“Repl”界面我们就可以进行一些简单的计算和操作，每一次都会返回一个结果eg:`res0:Int=19`（该信息体现了参数的定义，`val|var 参数名：参数类型=参数值`，该地方省略了val）。所以我们就可以通过参数名res0使用该值。
> res0(res1,res2...)　　#为返回值名称
> Int(Double,String....)　　#为返回值类型

## 变量定义

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325194130.png)

**scala有两种声明变量的方式**，`var`和`val`。`val类是于Java中的final变量`，一旦初始化就不能修改,例如上图中msg4;而var声明的变量就可以多次被赋值,scala建议声明为val。
在声明变量时也可以不指定类型，scala自己会进行`类型推断`，判断出“Word”为String类型（java.lang.String）。

**`懒值`** ，当val被声明为lazy时。它的初始化将被推迟，直到我们首次使用它，eg：
``` scala
lazy val words = scala.io.Source.fromFile("/use/word").mkString
```

## 变量类型

1. **scala中有7种数值类型**：`Byte`、`Char`、`Short`、`Int`、`Long`、`Float`、`Double`和`Boolean`，这类用法和java的基本类型类似。只是`scala这些类型是类`，它不区分引用类型和基本类型;
2. 对于字符串它使用的`java.lang.String`，但scala也有自己的扩展`StringOps`类；其他类型的一些扩展比如，RichInt、RichDouble、RichChar，还有java.math.BigIng、java.math.BigDecimal等;
3. 基本类型和包装类新之间的转换，这个scala编译器会自动完成，eg：创建一个Int[]数组，最后在虚拟机中得到的是int[];
4. 在scala中，数值类型之间的转换不是强制类型转换而是使用`方法`，eg：`toInt`、`toDouble`、`toChar等`。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326085134.png)

## scala脚本

脚本，就是一些简短的命令组合放在一个文件中，运行脚本就是按顺序执行文件中的语句。比如我们把这两行代码写到script.scala文件中：
![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325210208.png)

然后运行：

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325210612.png)

args(n) , 就可以接受到后面的参数（这个和java很像，java中main方法args[]同样能接收到）（注意：数组java是"[]"而scala中是"()"）。

## 扩展-Intellij使用

这里顺便讲一下使用`Intellij IDEA`开发scala：

> [下载](http://www.jetbrains.com/idea/)安装Intellij IDEA
> 安装Intellij的scala插件

菜单File--->Settings
![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325212935.png)
输入scala，然后点击右边的`install plugin`
![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325213129.png)
安装好插件后重启就可以新建项目了，File--->New--->Project,选择scala:
![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325214254.png)
输入项目名，选择项目地址和JDK和scala的SDK,Finish
![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325214355.png)
右键创建一个`scala class`，我们这里选择为Object
![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325215114.png)
写一个简单的例子，测试一下，okay!
![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325214646.png)


