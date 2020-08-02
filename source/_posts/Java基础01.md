---
title: Java基础01（常量、变量）
date: 2020-07-17 08:43:55
tags: Java
categories: Java基础
---

![](Java基础01/Java基础语法01.png)

<!--more-->

# HelloWorld类打印输出

```java
// 第一行的第三个单词必须和所在文件名称完全一样，大小写也必须一样
// public class后面代表定义一个类的名称，类是Java中所有源代码的基本组织单位
public class Hello {
    // 第二行的内容是万年不变的固定写法，代表main方法
    // 这一行代表程序执行的起点
    public static void main(String[] args){
        //第三行代表打印输出语句（屏幕显示）
        System.out.println("Hello World");
    }
}
```

## 注意事项

> - 类名和文件前缀要一致
> - 标识符命名规范参考[阿里巴巴java开发手册(提取码：qfo2)](https://pan.baidu.com/s/1-g36NRsPww6MFUf_VvNqyA)

# 基本数据类型

**四种基本数据类型**：整数型，浮点型，字符型，布尔型

**八大类**：byte, short, int（默认）, long, float, double（默认）, char, boolean

![基本数据类型](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200717090205.png)

## 注意事项

> - 变量不可以重复定义
> - 对于float和long，后缀F和L不要丢
> - 如果使用byte和short类型的变量，那么右侧的数据不能超过左侧类型的范围
> - 变量定义后，不可以直接使用，一定要赋值
> - 变量使用不可以超过作用域的范围【作用域】：从定义变量的一行开始，一直到直接所属的大括号结束为止
> - 可以一个语句创建多个变量

### byte和short超出数据类型

![short](Java基础01/short.png)

![byte](Java基础01/byte.png)

### 练习打字中...

```java
public class VariableNotice{
    public static void main(String[] args){
        int num1 = 10;
        // int num1 = 20; 名称不可以重复

        int num2;
        // System.out.println(num2); 未赋值，不可直接使用

        long num3 = 100L;// long后缀L
        System.out.println(num3);

        System.out.println(10.66F);// float后缀F

        byte b1 = 127;
        System.out.println(b1);
        // byte b2 = 128;
        // System.out.println(b2); // 超出数据类型
        short s1 = 32767;
        System.out.println(s1);
        //short s2 = 32768; // 超出数据类型
        //System.out.println(s2);

        {
            int num4 = 10;
            System.out.println(num3);
        } // 作用域包含大括号内，超出范围就不可调用

        // 再次定义num4不会出错
        int num4 = 100;
        System.out.println(num3);
    }
}
```