---
title: Scala--映射和元祖
date: 2016-03-26 15:33:53
tags: Scala
---

　　`映射`,就是键值对偶的集合，元祖就是n个对象的聚集，所以对偶就是n=2的元祖。简单来说就相当于java中的Map。

<!-- more -->

## 定义

``` scala
scala> val map = Map("a" -> 1 , "b" -> 2 ,"c" -> 3) //第一种定义方式
map: scala.collection.immutable.Map[String,Int] = Map(a -> 1, b -> 2, c -> 3)

scala> map("d") = 4   //赋值
<console>:12: error: value update is not a member of scala.collection.immutable.Map[String,Int]
       map("d") = 4
       ^
scala> val map2 = Map(("a",1),("b",2),("c",3))  //第二种定义方式
map2: scala.collection.immutable.Map[String,Int] = Map(a -> 1, b -> 2, c -> 3)
```
1. 定义对偶：使用 "`->`" 。
2. 直接使用Map是使用`immutable`下面的Map,此时这个map是`一个不可变的`。
3. 如果要定义一个`可变的Map`需要`scala.collection.mutable.Map`。

``` scala
scala> val canchage = scala.collection.mutable.Map("a" -> 1 , "b" -> 2 ,"c" -> 3)
canchage: scala.collection.mutable.Map[String,Int] = Map(b -> 2, a -> 1, c -> 3)

scala> canchage("d") = 4  //能正常的修改值

scala> canchage("d")   //获取值
res10: Int = 4
```
## 获取值

### 获取单个值

从上面的事例可以看出，获取值可以直接使用：`变量名("key")`。但如果没有改key怎么办？
``` scala
scala> map("d")
java.util.NoSuchElementException: key not found: d
  at scala.collection.MapLike$class.default(MapLike.scala:228)
  at scala.collection.AbstractMap.default(Map.scala:59)
  at scala.collection.MapLike$class.apply(MapLike.scala:141)
  at scala.collection.AbstractMap.apply(Map.scala:59)
  ... 33 elided
```
1. 当不存在key时，直接会抛出异常，可以使用`contains`进行判断;
2. 或者直接使用，`getOrElse("key",如不存在的值)`;

``` scala
scala> map.contains("d")
res14: Boolean = false

scala> map.getOrElse("d",66)
res15: Int = 66
```

### 迭代映射

有for基础后，再来看迭代就很简单了，直接看事例吧：

``` scala
scala> for((k,v) <- map) print(k+"->"+v + ", ")	//迭代键、值
a->1, b->2, c->3,

scala> for(k <- map.keySet) print(k+ ", ")	//迭代键
a, b, c,

scala> for(v <- map.values) print(v+ ", ")	//迭代值
1, 2, 3,
```
1. 基本语法就是：`for((k ,v) <- 映射 ) 处理k/v`
2. 如果只想获取值就迭代`values`,只想获取键迭代`keySet`

## 更新值

下面更新操作都是在可变的映射下完成，现在canchage中有key->a、b、c、d
``` scala
scala> canchage("d") = 7  //直接修改
scala> canchage("e") = 5  //不存在该值即添加该元祖
scala> canchage			//查看一下map中的数据
res23: scala.collection.mutable.Map[String,Int]=Map(e->5,b->2,d->7,a->1,c->3)
scala> canchage += ("e"-> 1 ,"f"->6) //这样同样可以修改和增加
res24: canchage.type = Map(e -> 1, b -> 2, d -> 7, a -> 1, c -> 3, f -> 6)

scala> canchage -= ("e","a")		//删除多个
res25: canchage.type = Map(b -> 2, d -> 7, c -> 3, f -> 6)
scala> canchage -= "b"	//删除单个
res26: canchage.type = Map(d -> 7, c -> 3, f -> 6)
```
1. 从上面的事例可以看出map的顺序在不断地改变，如果要创建一个不可变的Map使用：`scala.collection.mutable.LinkedHashMap`

2. 对于不可变的映射，可以重新再定义一个变量，后面添加需要修改和添加的值。

```

scala> map
res43: scala.collection.immutable.Map[String,Int] = Map(a -> 1, b -> 2, c -> 3)

scala> val mapch = map + ("a"->10 , "d"->14)		//mapch同样不可改变
mapch: scala.collection.immutable.Map[String,Int] = Map(a -> 10, b -> 2, c -> 3, d -> 14)

```



## 与java互转

``` java
import java.util.HashMap;
import java.util.Map;

/**
 * Created by xiaoxiaomo on 2016/3/26.
 */
public class JavaMap {

    public Map<String,Integer> getMap(){
        Map<String,Integer> map = new HashMap<String,Integer>() ;
        map.put("a",1);
        map.put("b", 2);
        return map ;
    }

    public void setMap(Map<String,String> map){
        for ( Map.Entry<String,String> entry: map.entrySet() )
            System.out.print(entry.getKey() + "->" +entry.getValue()+",");
    }
}

```
- scala转换代码
```  scala
import java.util.HashMap;
import java.util.Map;

/**
 * Created by xiaoxiaomo on 2016/3/26.
 */
public class JavaMap {

    public Map<String,Integer> getMap(){
        Map<String,Integer> map = new HashMap<String,Integer>() ;
        map.put("a",1);
        map.put("b", 2);
        return map ;
    }

    public void setMap(Map<String,String> map){
        for ( Map.Entry<String,String> entry: map.entrySet() )
            System.out.print(entry.getKey() + "->" +entry.getValue()+",");
		System.out.println();
    }
}
```
运行结果：
```
scala转java
a->1,b->2,c->3a,
java转scala
b->2,a->1,
```

## 元祖

`元祖`，就是不同类型值的聚集。`元祖的值是通过将单个的值包含在圆括号中构成的`。下面来看看元祖的一些使用（赋值、获取值）。

``` scala

scala> ("blog",".","xiaoxiaomo",19)
res31: (String, String, String, Int) = (blog,.,xiaoxiaomo,19)

scala> res31._1   //可以看出元祖的下标是从1开始，获取值使用“._”
res32: String = blog

scala> res31 _3	//第二种获取元祖方法“ _”，注意中间有一个空格
warning: there was one feature warning; re-run with -feature for details
res33: String = xiaoxiaomo

```                          
还有另一种获取元祖的方式，叫做`模式匹配`。这种方式可使一个方法变相的返回`多个返回值`，事例如下：

``` scala

scala> val (a,b,c,_) = res31 //不想匹配的值使用“_”
a: String = blog
b: String = .
c: String = xiaoxiaomo  

scala> a
res34: String = blog

scala> c
res35: String = xiaoxiaomo

``` 
## 拉链操作

`元祖`可以把很多值关联起来，以便统一处理。`对于这种链式处理，我们还可以使用zip`,还**可以让两个数组组合成一个对偶数组**，然后对偶数组可以`toMap`转为映射。eg：

``` scala
scala> var k = Array("a","b","c")	//数组1
k: Array[String] = Array(a, b, c)

scala> var v1 = Array(7,8,9)	//数组2
v1: Array[Int] = Array(7, 8, 9)

scala> k.zip(v1)		//两个数组组合成一个对偶数组
res37: Array[(String, Int)] = Array((a,7), (b,8), (c,9))

scala> res37.toMap		//对偶数组转为映射
res38: scala.collection.immutable.Map[String,Int] = Map(a -> 7, b -> 8, c -> 9)
```                                                    
- 注 ：
如果两个数组的长度不一致，会以长度短的为准，长的数据会丢失。

``` scala
scala> var v = Array(7,8,9,10)
v: Array[Int] = Array(7, 8, 9, 10)

scala> k.zip(v)
res39: Array[(String, Int)] = Array((a,7), (b,8), (c,9))

scala> v.zip(k)
res41: Array[(Int, String)] = Array((7,a), (8,b), (9,c))
```                                     