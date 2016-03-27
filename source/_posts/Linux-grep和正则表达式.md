---
title: Linux--grep和正则表达式
date: 2016-03-17 14:50:55
tags: Linux
---

　　`grep`（Global search REgular expression and Print out the line）英文有点长，`全局搜索正则表达式并打印出匹配的行`。从字面意思就知道一个很强大的文本匹配工具，可以通过正则来匹配，并且把匹配的行打印出来。

<!-- more -->

## **grep** 
语法
``` bash
grep [-acinv] [--color=auto] [-A n] [-B n] '匹配字符串' 匹配文件
```

常用参数说明
> **-c** ：#统计匹配次数
> **-i** ：#忽略大小写
> **-n** ：#显示行号
> **-v** ：#反选
> **--color** :#高亮匹配字段，可自定义
> **-A** ：#显示匹配行之后n行的信息，After,必须指定n
> **-B** ：#显示匹配行之前n行的信息，Before,必须指定n
> 注意：匹配的字段最好用''单引号，避免和shell元字符冲突。

eg.

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160317154131.png)

在当前目录下（以“.class”结尾的文件），匹配‘Thread’字符串，并显示出行号，高亮以及匹配字符后两行。


## **正则表达式**

### **常用正则表达式**


> **.** 匹配任意一个字符 #eg：grep 'a.r'text，会匹配arr,不会匹配ar。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160317163701.png)

> **\*** 前面字符出现0-n次。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160317163525.png)



> **[]** 匹配括号中的任意一个 

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160317165905.png)

*  [0-9]会匹配0-9
*  [a-z]会匹配a-z
*  [A-Z]会匹配A-Z
*  [0-9A-Z]会匹配0-9和A-Z
*  [[:space:]]会匹配空格
*  [[:punct:]]会匹配标点符号

> **\{n,m\}** 匹配前面字符重复n,m,次

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160317170706.png)

> **[^]** 匹配非字符串，#eg：grep '[^java]' text,匹配非java字符串。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160317170841.png)

> **^** 匹配以什么开头的行 
> **\$** 匹配以什么结尾的行 #eg：grep -n 'sleep\$' text。
> **\<** 匹配以什么开头的单词 
> **\>** 匹配以什么结尾的单词

### **扩展正则表达式**

可以通过-E参数使用grep的扩展正则表达式，等于egrep.


> **?** 匹配前面字符，0，1次。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160317165437.png)

> **+** 匹配前面字符，1-n次。eg：grep -E 'a+r' text。会匹配ar,aar等。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160317164242.png)

> **|** 匹配多个字符串

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160317171543.png)

> **()** 匹配括号中的字符串

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160317172007.png)
