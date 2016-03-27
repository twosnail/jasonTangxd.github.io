---
title: Scala--控制结构和函数
date: 2016-03-25 22:04:26
tags: Scala
---

　　本篇博客，将介绍scala的`条件表达式`，`循环`以及`函数`。主要是对这些表达式和语句结构的熟悉，需要多练习。在scala中表达式（3+4）和语句（if语句）是不同的概念，`表达式有值，语句执行动作`。记住，scala几乎所有构造出来的语法结构都有值。

<!-- more -->

## 条件表达式

`if/else`的表达式语法和java类似，只是需要注意的是：
1、if/else有返回值
2、scala代码结尾不需要“；”，除非一行要写多条语句，这个和`Python`类似。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325223536.png)

上图中，在scala脚本中,打印出了if的返回值0。


## 块语句

在scala中“`{}`”包含的一系列表达式，叫做块语句，`块中最后一个表达式的值就是块的值`。
![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325233121.png)

## while循环

`while循环`，和java的while和do循环相同，这里就不过多讲解了，实例如下图所示。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325234700.png)

**在"Repl"中写多行代码的时候**，每写一行敲一下“回车键”然后它会自动去识别程序是否结束，直到你真正的写完代码，有时候不是很方便；
还有一种粘贴的方法，输入`:paste`然后就可以随意的写代码了，写完后`Ctrl+D`退出并运行代码，如上图所示。

## for循环

### for基础

语句结构：

``` bash
for( i <- 表达式 )  #让变量i遍历<-右边的表达式的所有值，i具体执行取决于表达式
　　循环体
```

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325235656.png)

在`for循环的变量之前没有val或var的指定，该变量的类型是集合的元素类型`。循环变量的作用域一直持续到循环结束。
`until`：返回一个并不包含上线的区间。
scala中没有**break**和**continue**来退出循环，我们可以这样**操作**：

> 1. 使用Boolean的变量控制。
> 2. 使用嵌套函数，可以从函数当中return。
> 3. 使用Breaks对象的break方法。

- eg：

``` scala
breakable{
 for(...){
  if（...） break ;//#退出breakable块
} }
```
### for进阶

1. 在for循环“（）”中可以使用**多个生成器**， 用“；”隔开；
2. 并且每一个生成器都可以带一个**`守卫`**（`if开头的Boolean表达式`）；
3. **可以使用变量**，如下图所示：

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326003214.png)

- 如果for循环的循环体以yield开始，该循环就会构造出一个集合，每次迭代就生成一个集合的值。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326003916.png)

## 函数

### 基本语法

语法如图：

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325202143.png)(图来源于：Scala编程)

1. 函数必须指定`参数的类型`。
2. 函数只要不是递归的就不需要指定`返回值类型`（因为无法推断出递归函数的类型）。
3. 在函数中，不需要使用return。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160325202002.png)

### 函数参数

在函数中，我们可以使用`默认参数`。函数调用时：
> 1、如果没用给出所有参数，函数会使用默认参数（后面不够的参数使用默认值）。
> 2、也可以指定参数名，参数名不需要按顺序排列。
> 3、如果混合使用（未名参数和带名参数），只要未名参数排在前面即可。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326010934.png)

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326010958.png)

> 4、**变长参数**，可以接受多个参数

``` scala
def sum(args:Int*) = {
 var result = 0 ;
 for(arg <- args) result+=arg
  result
}
```
调用函数，sum(3,4,6,23,3),函数得到的是一个Seq类型的参数，注意调用函数是传入的参数不能是一个区间，eg：
sum(2 to 9)是不可以的，应该为sum(2 to 9:_*);

## 过程

在scala中，如果函数没有返回值，那么该返回值类型我们可以用`Unit`来表示，这种`没有返回值的函数我们称之为过程`。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326093418.png)

上面**省略了Unit**,由于没有返回值也可以**省略“=”号**，下面语句相同：

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326093708.png)

