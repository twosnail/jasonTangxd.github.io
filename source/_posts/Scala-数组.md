---
title: Scala--数组
date: 2016-03-26 10:19:15
tags: Scala
---

　　`数组`，存储相同类型元素的连续集合。在JVM中，scala以java数组的方式实现，Array[Int],Array[String]等分别对应着java的基本类型数组int[]、String[]。

<!-- more -->

## 数组语法

- 语法：

``` scala
val|var 变量名：Array[变量类型] = new Array[变量类型](长度)　　#数组的定义
val|var 变量名 = new Array[变量类型](长度)　　#简化形式（常用）
val|var 变量名 = Array(初始化值)　　#直接初始化值，自动会进行类型推断
```
eg：

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326103721.png)


![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326104027.png)


从上面的例子中可以看到：
1. 当我们定义数组时，如果没有初始化值它会根据数据的长度`自动初始化`，设置默认参数；
2. 数组可以自己进行类型推断，当类型不一致时，会为`Any类型`；
3. `提供了初始值就不需要new`;
4. `定长数组必须指定数组长度`；

还需要注意的是，如果数组声明为val那么该数组的值是可以改变的；只是该变量不能重新被赋值，即**变量指定的数组对象地址不能改变，数组对象的值可以变**。

- 变长数组

变长数组，使用`ArrayBuffer`也叫`数组缓冲`。就是定义一个可以改变的数组，在定义时**可以不指定数组长度**。

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326111826.png)

上图中，虽然是val定义的变量，但是我们还是可以修改值。
1. 定义变长数组时，“**()**”可以省略。记住`省略“()”后就不能省略new,省略new就不能省略“()”`在下图事例中，第一种定义就无效；

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326112222.png)

2. 给数组赋值时，可以使用“+=单个参数|(多个)”，“++=数组”在尾部追加数据；
3. 赋值完成后，可以使用toArray方法转为数组，当然也可使用toArrayBuffer转回去；
4. 数组常用方法，remove(...),insert(...),trimEnd;

## 数值遍历

之前我们已经讲过for循环，使用上面定义的**ab**数组做一下遍历

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326113707.png)

注意：
1. 数组的小标从0开始，所以最大小标为length-1，不然会越界，通常使用`unitl`；
2. 获取数组元素的时候使用“`()`”,和java不同；
3. **使用yield可以创建一个新的集合，原始集合并不受影响**，注意**yield在“{}”的后面**，“{}”也可省略；
4. 当然同样可使用“**带刀侍卫**”(●'◡'●)，侍卫也能获取元素；

## 常用算法

具体内容可阅读`scaladoc`文档，这里简单的举例

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326115846.png)

## 多维数组
多位数组和java的数组类似，里面也是使用了数组。二维数组使用关键只`ofDim`方法：

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160326131111.png)

## 与java互转
与java互转操作，在后面应该会常用。在scala中`Scala.collection.JavaConversions`里的有隐式转换方法。下面来写一个例子：

``` java
import java.util.ArrayList;
import java.util.List;

/**
 * 一个简单的java代码demo
 * Created by xiaoxiaomo on 2016/3/26.
 */
public class JavaArraList {

    public List<String> getListStr(){ //会返回一个List<String>类型的集合
        List<String> list = new ArrayList<String>() ;
        list.add("Hello");
        list.add("word");
        return list ;
    }

    public void setListStr(List<String> arrList){//需要传递一个List集合
        for ( String str : arrList )
            System.out.print(" " + str);
        System.out.println();
    }
}
```
- scala操作

``` scala
import scala.collection.JavaConversions
import scala.collection.mutable.ArrayBuffer

/**
 * Created by xiaoxiaomo on 2016/3/25.
 */
object TestDemo {

    def main(args: Array[String]): Unit = {
      val sca = ArrayBuffer("Hl", "ooo", "woddd") ;
      //
      println("scala转java")
      new JavaArraList().setListStr(JavaConversions.bufferAsJavaList(sca));
      //
      println("java转scala")
      val j2s =JavaConversions.asScalaBuffer(new JavaArraList().getListStr()) ;
      for( i <- 0 until j2s.length )  print( " " + j2s(i) )
    }
}
```
- 运行结果

```
scala转java
 Hl ooo woddd
java转scala
 Hello word
```