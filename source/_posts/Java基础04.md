---
title: Java基础04（方法）
date: 2020-07-19 13:29:40
tags: Java
categories: Java基础
---

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200719141905.png)

<!--more-->

# 方法的基本格式

## 无参数

```java
public class DemonWithParamter{
    public static void main(String[] args){
        // 使用方法需要在main函数中调用
        
    }
    
    public static void method01(){
        System.out.println("这是无参数输入的方法") // 直接调用该方法 输出语句
        
    }
}
```

## 有参数

```java
public class DemonWithoutParamter{
    public static void main(String[] args){
        // 使用方法需要在main函数中调用
        
    }
    
    public static int method02(int a, int b){
        System.out.println("这是有参数输入的方法")
            return a + b; // 输出类型为int类型
        
    }
}
```

## 有无return

> 对于void, return可写可不写，但是在void条件下，return后不可以跟任何输出值；
>
> 定义了输出类型的方法，需要进行return输出

## 注意事项

> 1. 方法应该定义在类当中，但是不可以在方法中再定义方法。不能嵌套
> 2. 方法定义的前后顺序无所谓
> 3. 方法定义之后，如果希望执行，一定要调用：单独调用，打印调用，赋值调用
> 4. 如果方法有返回值，那么必须写 "return 返回值"，不能没有
> 5. return后面的返回值类型，必须和方法的返回值类型，对应起来
> 6. 对于void没有返回值的方法，不能写return后面的返回值，只能写return。
> 7. 对于void方法的最后一行return也可以不写
> 8. 一个方法当中有多个return语句，但是必须保证只有一个被执行到

# 三种调用格式

> 1. 单独调用
> 2. 打印调用，System.out.println(方法名称（参数）)
> 3. 赋值调用：数据类型  变量名称 = 方法名称（参数）

```java
public class Demon02MethodDefine {
    public static void main(String[] args){
        // 单独调用
        sum(5,6);
        System.out.println("======================");

        // 打印调用
        System.out.println(sum(10,20));

        // 赋值调用
        int input = sum(5,6);

        System.out.println("======================");

        method(); // 无输出语句

    }

    public static int sum(int a, int b){
        int result = a + b;
        return result;
    }

    // 打印输出固定十次文本字符串
    public static void method(){
        for (int i = 0; i < 10; i++) {
            System.out.println("Hello World"+i);
        }
    }
}
```

# 方法重载

## 方法重载与下列因素有关

> 1. <font color=orange>参数个数</font>不同
> 2. <font color=orange>参数类型</font>不同
> 3. <font color=orange>参数的多类型顺序</font>不同

## 方法重载与下列因素无关

> 1. 与<font color=red>参数的名称</font>无关
> 2. 与<font color=red>返回值的类型</font>无关

其实常用的`println()`就是一个典型的方法重载，在IDEA中可以按住`ctrl`点击该命令，可以看到该命令的定义格式。

## 打字练习中...

```java
public class Demon07MethodOverload {
    public static void main(String[] args){
        System.out.println(sum(10, 20)); // 两数相加
        System.out.println(sum(10, 20, 30)); // 三个数相加
        System.out.println(sum(10, 20, 30, 40)); // 四个数相加

    }

    public static int sum(int a, int b){
        System.out.println("有两个参数即可");
        return a + b;
    }

    public static int sum(int a, int b, int c){
        System.out.println("有三个参数即可");
        return a + b + c;
    }

    public static int sum(int a, int b, int c, int d){
        System.out.println("有三个参数即可");
        return a + b + c + d;
    }


    public static int sum(int a, double b){
        return (int) (a + b);
    }

    public static int sum(double a, int b){
        return (int) (a + b);
    }

    public static int sum(double a, double b){
        return (int) (a + b);
    }


    // 错误写法：与方法的返回值类型无关
    /*public static double sum(int a, int b){
        return a + b;
    }*/

    // 错误写法：与参数的名称无关
    /*public static int sum(int x, int y){
        return x + y;
    }*/
}
```

# 一些练习

```java
// 定义个一个方法  求出1-100所有的数字和

public class Demon04Sum {
    public static void main(String[] args){
        System.out.println(sum(1,100));

    }

    // 定义了【a,b】的所有数字和
    public static int sum(int a, int b){
        int count = 0;
        for (int i = a; i < b+1; i++) {
            count +=i;
        }
        return count;
    }
}
```



```java
/*
* 题目要求：
* 定义一个方法，用来打印指定次数的HelloWorld
* */
public class Demon05MethodPrint {
    public static void main(String[] args){
        print(2);
    }

    public static void print(int num){
        for (int i = 0; i < num; i++) {
            System.out.println("HelloWorld"+(i+1));
        }

    }
}
```



```java
/*
* 题目要求：
* 比较两个数据是否相等
* 参数类型分别式两个byte,两个short，两个int，两个long类型
* 并在main方法中测试
* */

public class Demon08MethodOverloadSame {
    public static void main(String[] args){
        byte a = 10;
        byte b = 20;
        System.out.println(isSame(a , b));

        System.out.println(isSame((short) a, (short) b));

        System.out.println(isSame(15,20));

        System.out.println(isSame(20L,20L));



    }

    public static boolean isSame(byte a, byte b){
        System.out.println("两个byte参数的方法执行！");
        return a == b;
    }

    public static boolean isSame(short a, short b){
        System.out.println("两个short参数的方法执行！");
        return a == b;
    }

    public static boolean isSame(int a, int b){
        System.out.println("两个int参数的方法执行！");
        return a == b;
    }

    public static boolean isSame(long a, long b){
        System.out.println("两个long参数的方法执行！");
        return a == b;
    }


}
```