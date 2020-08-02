---
title: Java基础06（数组-二维数组）
date: 2020-07-21 14:00:02
tags: Java
categories: Java基础
---



![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200721141209.png)

家庭收支小项目见[JavaLearning](https://github.com/YuanbaoQiang/JavaLearning)仓库。

<!--more-->

# 基本格式

## 动态初始化

### 方式一

```java
public class ArrayTwoDynamicDefine01{
    public static void main(String() args){
        int[][] array1 = new int[4][3]
    }
}
```

### 方式二

```java
public class ArrayTwoDynamicDefine02{
    public static void main(String() args){
        int[][] array2 = new int[4][]
    }
}
```

## 静态初始化

### 方式一

```java
public class ArrayTwoStaticDefine01{
    public static void main(String() args){
        int[][] array3 = new int[][]{{1,2,3},{49,8,63,3},{8,62,3,6}}
    }
}
```

### 方式二

```java
public class ArrayTwoStaticDefine02{
    public static void main(String() args){
        int[][] array4 = {{1,2,3},{49,8,63,3},{8,62,3,6}}
    }
}
```

# 基本用法

## 元素调用

对于上述array2和array3数组进行调用

```java
System.out.println(arr3[0][1]); // 2
System.out.println(arr3[2][1]); // 62
System.out.println(arr2[2][2]); // null 还未指定存放的元素
```

注意，对于动态数组方式二定义的数组，需要先对内存元素进行定义，否则，将会出现空指针异常报错：

```java
arr2[1] = new String[4];
System.out.println(arr2[1][0]); // 得先对 arr2[1]进行定义，否则出现空指针异常
```

## 数组长度获取

```java
// 获取数组的长度
System.out.println(arr3.length); // 3
System.out.println(arr3[0].length); // 3
System.out.println(arr3[1].length); // 4
```

## 二维数组的遍历

遍历array3

```java
for (int i = 0; i < array3.length; i++) {
    for (int j = 0; j < array3[i].length; j++) {
        System.out.print(array3[i][j]+" ");
    }
    System.out.println();
}
```

# 内存解析

![image-20200721221224513](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200721221224.png)

