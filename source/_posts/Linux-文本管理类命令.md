---
title: Linux--文本管理类命令
date: 2016-03-16 15:05:48
tags: Linux
---
## **文件信息**

### **文本统计信息**

ls命令可以查看，以及批量查看文件的某些信息，但是文件的状态信息还是无法查看。stat,可以查看文件的状态信息。

<!-- more -->

`stat`

![stat](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160317185329.png)

- 访问：access
- 修改：modify（修改，指的是修改了文件的内容）
- 改变：change，metadata(元数据)（改变，指的是改变了文件的属性，或者说元数据）

### **文本查看命令**

`cat`、`tac`、`more`、`less`、`head`、`tail`

``` bash
cat  #链接并显示,一次显示整个文件
tac  #和cat相反，倒着显示
```
> cat fileName : 一次显示所有文件内容
> cat > fileName : 从键盘创建一个文件（ctrl+c，保存代码）
> cat f1 f2 > fileNmae : 合并文件内容（技巧）
> cat -n：在显示的时候给每一个行编号
> cat -E：显示每一行的行结束符有，linux的文本行结束符为“$”，和windows有区别。(如果想翻屏，就shift+PaUp/PaDn）

``` bash
more  #分屏翻页（支持向后翻，不支持向前翻），常常配合管道命令使用
less  #和more相似，可前后翻。eg：ps -ef|less，（#使用q退出）
```

``` bash
head  #查看文件前n行（默认10行）
tail  #查看文件后n行（默认10行）
```
> tail -n num fileName : 查看文件前num行。
> tail -f：查看文件尾部，不退出，等待文件追加内容。常用于查看日志！
  
## **文本处理** 
 
### **文本处理**

`cut`、 `join`、`sed`、`awk`
    
``` bash
cut ：剪切命令，一般配合管道命令使用，
```
> -d：字节，指定字段分隔符（默认为一个空格）。
> -c：字符，
> -f：区域，指定要显示的字段

eg.

- -f 1：显示第一个字段
- -f 1,3：显示第一个和第三个字段（离散表示法）
- -f 1-3：显示一到三的字段（连续表示法）
![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160316160346.png)

### **文本排序** ###
    
``` bash
sort：（默认字母升序）
```

> -n 排序数字
> -r 逆向排序
> -t  ：以什么为分隔符
> -k    :从哪个字段开始
> -u：排序后相同的行只显示一次
> -f：忽略字符大小写
    
``` bash
uniq：报告重复行（相邻并相同才算做向同行）
```

> -d：只显示重复行
> -D：显示所有重复行
> -c：把所有行取出来，并显示次数
    
### **文本统计** ###
    
``` bash
wc(word count) 
```

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F42190026-98ac-43aa-a690-f9122f44df3f.png)

分别为：行 单词数 字节/字符数

> -l：行
> -w：单次数
> -c：字节
> -m：字符
> -L：最长的一段包含了多少字符

eg.

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160316161803.png)


### **字符处理** ###
    
``` bash
tr  #转换或删除字符，可以实现set的基本功能，替换，删除，去重
```

> tr [OPTION] SET1 [SET2]

eg.

`tr 'a-z' 'A-Z' < /etc/passwd`  #把passwd中所有信息转成大写。
`tr -d 'ab' < fileName `        #把文件中包含a和b的删除掉。
