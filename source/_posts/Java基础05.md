---
title: Java基础05（数组-单维）
date: 2020-07-20 11:00:52
tags: Java
categories: Java基础
---



![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200720123008.png)

<!--more-->

# 基本格式

## 动态初始化

> 格式：数据类型[]  数组名称 = new 数据类型 [数组长度]

```java
public class Demon01Array {
    public static void main(String[] args){
        int [] arrayA = new int[300];
    }
}
```

此方法虽然只定义了数组的长度，未定义内容，但是系统默认会有初始值。

|   数据类型   |    0     |
| :----------: | :------: |
|    整数型    |   0.0    |
|    字符型    | '\u0000' |
|    布尔型    |  false   |
| 引用数据类型 |   null   |

## 静态初始化

标准格式

> 数据类型[]  数据名称 = new 数据类型[] {元素1，元素2，元素3...}

```java
public class Demon02Array {
    public static void mian(String[] args){
        int[] arrayA = new int[] {5,10,20};
    }
}
```

省略格式

> 数据类型[] 数组名称 = {元素1，元素2，。。}

```java
public class Demon02Array {
    public static void mian(String[] args){
        int[] arrayA = {5,10,20};
    }
}
```

## 注意事项

> 1. 静态初始化没有直接指定长度，但是仍然会自动推算到长度
> 2. 静态初始化标准格式可以拆成两个步骤（先定义数组名称，后定义长度或内容）
> 3. 动态初始化也可以拆成两个步骤
> 4. 静态初始化一旦使用省略格式，就不能拆分成两个步骤

# 内存划分

## Java的内存需要划分为5个部分

> 1. 栈（stack）：存放的都是方法中的局部变量。局部变量：方法的参数，或者是方法{}内部分变量。作用域：一旦超出作用域，立即从栈内存当中消失
> 2. 堆（Heap）：凡是new出来的东西，都在堆当中，堆内存中的东西都有一个地址值：16进制
> 3. 方法区（Method Area）：存储.class相关信息，包含方法的信息
> 4. 本地方法栈（Native Method Stack）：与操作系统相关
> 5. 寄存器（pc Register）：与cpu相关

## 一个数组的内存图

![02-只有一个数组的内存图](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200720123706.png)

## 两个数组的内存图

![03-有两个独立数组的内存图](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200720123719.png)

## 两个引用指向同一个数组的内存图

![04-两个引用指向同一个数组的内存图](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200720123933.png)

以下的arrayA和arrayB实际时同一个数组，arrayA和arrayB只是数据的名称，最关键的还是是否有new，是否有新的内存地址产生。

```java
public class Demon03ArraySame {
    public static void main(String[] args){
        int[] arrayA = new int[3]; // 动态初始化
        System.out.println(arrayA); // 地址值
        System.out.println(arrayA[0]); // 0
        System.out.println(arrayA[1]); // 0
        System.out.println(arrayA[2]); // 0
        System.out.println("=======================");

        // 改变数组当中元素的内容
        arrayA[1] = 10;
        arrayA[2] = 20;
        System.out.println(arrayA); // 地址值
        System.out.println(arrayA[0]); // 0
        System.out.println(arrayA[1]); // 10
        System.out.println(arrayA[2]); // 20
        System.out.println("=======================");


        int[] arrayB = arrayA; // 动态初始化
        System.out.println(arrayB); // 地址值
        System.out.println(arrayB[0]); // 0
        System.out.println(arrayB[1]); // 10
        System.out.println(arrayB[2]); // 20
        System.out.println("=======================");

        // 改变数组当中元素的内容
        arrayB[1] = 100;
        arrayB[2] = 200;
        System.out.println(arrayB); // 地址值
        System.out.println(arrayB[0]); // 0
        System.out.println(arrayB[1]); // 100
        System.out.println(arrayB[2]); // 200


        // 此时原本的arrayA数值已经发生了改变
        System.out.println(arrayA[1]); // 0
        System.out.println(arrayA[2]); // 0

    }
}
```

# 数组在方法中的运用

## 作为输入

方法的输入参数中可以定义一个数组。

调用方法时，实际就是将数组的地址值传递给方法，然后根据地址来访问数组内的元素。

```java
public class Demon07ArrayParameter {
    public static void main(String[] args){
        int[] array = {10, 20, 30, 40, 50, 60};
        System.out.println(array); // 地址值
        printArray(array); // 传递进去的就是array的地址值

    }

    // 定义一个方法
    public static void printArray(int[] array){
        for (int i = 0; i < array.length; i++) {
            System.out.println(array[i]);
        }
    }

}
```

## 作为输出

可以利用数组，实现在方法中输出多个返回值。

原理同上，调用也是通过输出数组的地址值，然后根据地址访问元素。

```java
public class Demon08ArrayReturn {
    public static void main(String[] args){
        int[] result = calculate(10, 20, 30);
        System.out.println("result的地址值："+ result);
        System.out.println("总和为"+result[0]);
        System.out.println("平均数为"+result[1]);

    }

    public static int[] calculate(int a, int b, int c){
        int sum = a + b + c; //总和
        int ave = sum / 3; // 平均数

        int [] array = new int[2];
        array[0] = sum; // 总和
        array[1] = ave; // 平均数

        System.out.println("array的地址值："+array);
        return array;
    }
}
```

# 一些练习

## 求最值

```java
/*求出数组中的最大值*/
public class Demon05ArrayGetMax {
    public static void main(String[] args){
        int array[] = {1,1,5,15,1,4,7,3,5,67,4,6,0,7,8,3,4,5,3,6,3,7,9,49,8,5};

        // 求最大值
        int max = array[0];
        for (int i = 1; i < array.length; i++) {
            max = array[i] > max ? array[i]:max;
        }
        System.out.println("最大值为："+ max);


        // 求最小值
        int min = array[0];
        for (int i = 1; i < array.length; i++) {
            min = array[i] < min ? array[i]:min;
        }
        System.out.println("最大值为："+ min);
    }
}
```

## 数组元素反转

![07-数组元素反转的思路](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200720130519.png)



```java
/*
* 数组元素的反转：
* 本来的样子：[1,2,3,4]
* 之后的样子：[4,3,2,1]
* */

public class Demon06ArrayReverse {
    public static void main(String[] args){
        int array[] = {10,20,30,50,60};

        // 遍历打印数组本来的样子
        for (int i = 0; i < array.length; i++) {
            System.out.print(array[i]+" ");
        }
        /*
        * 初始化语句：int min = 0, max = array.length-1
        * 条件判断: min < max
        * 步进表达式: min++, max--
        * */

        for(int min = 0, max = array.length-1; min < max; min++, max--){
            int temp = array[min];
            array[min] = array[max];
            array[max] = temp;
        }

        System.out.println();

        // 再次遍历打印数组
        for (int i = 0; i < array.length; i++) {
            System.out.print(array[i]+" ");
        }

    }
}
```