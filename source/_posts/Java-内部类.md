---
title: Java--内部类
date: 2016-03-27 12:59:55
tags: Java
---

　　一提到写Java的博客，就有点犯困，原因是：`大牛太多`！自己写好一篇博客感觉压力挺大的，因为随便一搜就是一大堆优秀的博客，笔记Java这个生态系统发展这么多年已经很完善了。我在这里只是做一些总结和完善吧，写之前我也阅读过很多相关博客，不得不承认他们的优秀。

<!-- more -->

`内部类`，就是在一个类里面再定义一个类。分为四大类：`成员内部类`、`匿局部内部类`、`匿名内部类`和`静态内部类`。

## 成员内部类

`成员内部`：`定义一个类位于另一个类的内部`，内部类能无限制的访问`外围类公有/私有`成员变量和方法。如下：

``` java
class Demo01 {
    public static void main(String[] args)  {
        Outer o = new Outer();
        o.method();
		//如果，Inter为public则调用show方法时，使用如下代码
		//Outer.Inter i = new Outer().new Inter();
        //i.show();
    }
}

class Outer { //外部
    private String name = "momo" ; //Outer.this.name
    int num = 10;//Outer.this.num
    private class Inter { //编译源码会发现=>内部类,持有一个外围类的引用
        int num = 20;//this.num
        public void show(){
            int num = 30;//num
		//外围类的private，name成员变量
            System.out.println("name:"+Outer.this.name+" Outer.this.num:"+
                    Outer.this.num+" this.num:"+this.num +" num:"+num );
        }
    }
    //
    public void method(){
        Inter i = new Inter(); //提供一个访问入口
        i.show();
    }
}
```
- 运行结果：name:momo Outer.this.num:10 this.num:20 num:30


## 局部内部类

`局部内部类`：`嵌套在方法和作用于内的`。主要是应用于想创建一个类来辅助我们的解决解决比较复杂的问题，又不希望这个类是公共可用的，所以就产生了局部内部类。局部内部类和成员内部作用域不同，它`只能在该方法和属性中被使用，出了该方法和属性就会失效`。

``` java
public class Demo02 {
    public static void main(String[] args){
        Outer02 o = new Outer02();
        o.method();
    }
}

class Outer02 {//外部
    int num = 10;
    public void method() {
        int num = 20; //在这里定义的num内部类访问不到
        class Inter02 {
            private int num = 30 ;
            public void show(){
                System.out.println("Outer02.this.num:"+Outer02.this.num +
                        " this.num:"+this.num+" num:"+num);
            }
        }
        Inter02 in = new Inter02();
        in.show();
    }
}
```
- 运行结果：Outer02.this.num:10 this.num:`30` num:30

> 成员内部类中不能存在任何public、protected、private以及static的变量和方法；

## 匿名内部类

`匿名内部类`：`必须要继承一个父类或者实现一个接口`，只是用一次，通常用来简化代码。没有class关键字，因为匿名内部类是直接使用new来生成一个对象的引用。当然这个引用是隐式的，没有构造方法。

- 匿名内部类的结构：

``` java
	new 父类构造器（参数列表）| 实现结构（）{
		//重写父类的方法或实现接口的方法
		//目的：在这个地方想对某个类有特殊实现。
		//对于java任何类或接口，都可以声明一个匿名内部类继承或实现
	}
```

``` java
public class Demo03 {
    public static void main(String[] args) {
        Outer03 o = new Outer03();
        o.method("xiaoxiaomo",23);
    }
}
//抽象类
abstract class AbsDemo {
    public abstract void show();
}

class Outer03 {
    public void method(final String name,int num){
		//new AbsDemo(){//匿名内部类,第一种调用方式
		//	public void show(){
		//		System.out.println(name);
		//	}
		//}.show();

        AbsDemo a = new AbsDemo(){//第二种
            public void show(){
                System.out.println(name /*+num*/);
            }
        };  //分号不能省
        a.show();
    }
}
```

> - 匿名内部类是没有访问修饰符的。
> - `new 匿名内部类()`;这个类首先是要存在的。如果我们将那个AbsDemo抽象类注释掉，会编译出错。
> - 注意method()方法的形参，第一个形参是用final修饰的，而第二个却没有（使用就会编译出错）。所以当方法的形参需要被匿名内部类使用，那么这个形参就必须为final。



## 静态内部类。

`静态内部类`：使用static修饰的内部类称之为静态内部类。静态内部类与非静态内部类之间存在一个最大的区别，就是`非静态内部类在编译完成之后会持有一个外围类的引用，但是静态内部类却没有`。没有这个引用就意味着：

> 它的创建是不需要依赖于外围类的。
> 它不能使用任何外围类的非static成员变量和方法。

``` java
public class Demo04 {
    public static void main(String[] args) {
        Outer04.Inner i = new Outer04.Inner();
        i.method();
    }
}

class Outer04 {
    private String name = "xiaoxiaomo";
    private static int num = 8 ; //静态

    static class Inner{
        //String s = name ; //不能使用非静态变量
        String str  = "这里可以" ;
        public void method(){
            System.out.println("num:"+num+" str:"+str);
        }
    }
}
```

## 内部类的作用

```
方便将存在一定逻辑关系的类关联到一起，并可以实现隐藏。比如一般的类不能进行私有化操作。
内部类是的多继承的解决方案更加完善。比如我们可以在第一个类里面定义多个内部类分别继承不同的类。
能无条件的访问外围类所有元素
很方便的编写多线程和事件驱动程序。
```

- 参考资料：
- [http://www.cnblogs.com/chenssy/p/3388487.html](http://www.cnblogs.com/chenssy/p/3388487.html)
- [http://blog.csdn.net/chenssy/article/details/13170015](http://blog.csdn.net/chenssy/article/details/13170015)
- [http://www.cnblogs.com/nerxious/archive/2013/01/25/2876489.html](http://www.cnblogs.com/nerxious/archive/2013/01/25/2876489.html)