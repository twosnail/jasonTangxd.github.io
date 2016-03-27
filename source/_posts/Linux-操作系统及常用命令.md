---
title: Linux--操作系统及常用命令
date: 2016-03-16 14:10:57
tags: Linux
---

　　主要介绍操作系统上一些`常见命令`，比如创建文件目录mkdir，查看目录下文件ls，系统环境变量，系统时间，帮助文档等。

<!-- more -->

## 目录/文件简介

路径：从指定起始点到目的地的所经过的位置。
命令规则：
```
长度不能操作255个字符；
不能使用“/”当文件名；
严格区分大小写
```
## 目录/文件查看

> 查看目录文件 `ls`：

``` bash      
ls -l #长格式，可以简化为，ll；
ls -h #做单位换算，human can readable；
ls -a #以点开头的文件（包括隐藏文件、.表示当前目录、..表示上级目录）；
ls -A #显示全部文件（不包括.和..）；
ls -d #显示自身属性；
ls -i #index node，inode(显示文件唯一序号)；
ls -r #逆序显示；
ls -R #递归显示（recursive）；
```

- eg：`ls -l`

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2Ff19aa739-0de8-499b-b978-bedd1bb1a849.png)

1. **第一位,表示`文件类型`**
```
- -：普通文件（f），如上图第二个文件；
- d：目录文件，如上图第一为文件目录；
- b：块设备文件（block）
- c：字节设备文件（character）
- l ：符号链接文件（sysbolic link ）
- p：管道命令（pipe）
- s：套接字文件（socket）
```
2. **文件权限**：紧接着后面9位，每三位一组，每一组（rwx）r：可读，w：可写：x:可执行
3. **文件硬链接次数**
4. **文件的属主**（owner）
5. **文件的所属组**（group）
6. **文件的大小**（size）,单位字节
7. **时间戳**（timestamp）:最近一次被修改的时间（文件内容）

其他基本命令：

> pwd　　#显示目录路径
> cd　　#切换目录，当前目录
> tree　　#查看目录树
> stat　　#查看状态

## 目录/文件操作

> `mkdir`：创建空目录

``` bash
-p： #递归创建，eg：mkdir -p test/test01/test02
-m： #创建文件夹时，指定权限。eg：mkdir -m 777 test03
-v： #创建文件夹时，展示详细信息。eg：mkdir -v test04
{}： #多级创建,eg：#mkdir -pv test05/a{x/m,y} 
```

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160327114247.png)

> `rmdir`：删除空目录

``` bash
-p： #删除多级非空目录
```

> `touch`：创建文件

``` bash
-a： #修改访问你时间（默认修改为当前时间）atime=access time
-m： #只更改变动时间，mtime=modify time
-t： #修改某个时间
```

> `rm`：删除文件/目录

``` bash
-i： #--interactive，进行交互式删除
-f： #--force，忽略不存在的文件，不给出提示
-r： #--recursive递归删除多级目录，eg:rm -rf /tmp #删除tem目录及其子目录全部文件
-v： #--verbose ，详细显示进行的步骤
```

## 环境变量

> 命令的内存空间，env
> 变量赋值
> eg：NAME=Tom(在内存中着一段空间，起名叫NAME,空间放的数据叫Tom),申请变量的过程，就是申请内存使用的过程。
> path：以冒号隔开的一对路径。
> hash：查看缓存

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2Facf4c7a3-9a2c-4ddf-aff9-5e78ee439f50.png)

`缓存，catch is king.保存的是hash列表。在key,value中的查找速度是O(1).O(1):表示查找时间，不会随着，数据的增加而递增。`

## 时间

``` bash
data：
```
> 硬件主板的震荡器，rtc   
> 硬件时钟：clock
> 系统时钟：date

``` bash
hwclock   #（写入时间）
```
> -w：读取系统时间到硬件中
> -s ：读取硬件时间到系统中

``` bash
cal：日历
```

## 帮助命令

在线文档
``` bash
info COMMAND(主要讲历史等)
文档：/usr/share/doc
```

> 内部命令：help COMMAND
> 外部命令：COMMAND --help
> 命令手册：manual
> man COMMAND
> whatis COMMAND
> 分章节
    1、用户命令（/bin , /usr/bin , /usr/local）
    2、系统调用
    3、库用户
    4、特殊文件（设备文件）
    5、文件格式（配置文件的语法）
    6、游戏 
    7、杂项（Miscellaneous）
    8、管理命令（/sbin,  /usr/sbin  , /usr/local/sbin），管理员，会修改硬件相关的信息

``` bash
man 命令:
```

> []   ：可选
> <>：必须有
> ...  ：可以出现多次
> |   ：多选一
> {}  ：分组
> NAME：命令名称及功能简要说明
> SYNAPOSIS：用户说明，包括可用的选项
> DESCREPTION：命令功能的详细说明， 可能包括没一个选项的意义
> OPTIONS：选项
> FILES：此命令的相关配置
> BUGS：
> Examples：使用示例
> SEE ALSO：另外参考
