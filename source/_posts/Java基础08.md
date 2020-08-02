---
title: Java基础08（类、对象）
date: 2020-07-24 10:30:43
tags: Java
categories: Java基础
---



![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200724104113.png)

<!--more-->

# 面向对象（OOP）思想

> 面向对象编程：OOP (Object-Oriented Programmming)
>
> 面向对象分析：OOA (Object-Oriented Analysis)
>
> 面向对象设计：OOD (Object-Oriented Design)

面向对象是一种思想，是基于面向过程而言的，就是说面向对象是将功能等通过对象来实现，将功能封装进对象之中，让对象去实现具体的细节；这种思想是将数据作为第一位，而方法或者说是算法作为其次，这是对数据一种优化，操作起来更加的方便，简化了过程。

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200724105959.webp)

参考：

[OOA/OOD/OOP细讲](https://www.jianshu.com/p/224d8fc4d0f0)

[什么是面向对象（OOP）](https://www.jianshu.com/p/7a5b0043b035)

# 类

> 1. 定义类（考虑修饰符、名）
> 2. 编写类的属性 （考虑修饰符、属性 类型、属性名 、初始化值）
> 3. 编写类的方法 （考虑修饰符、返回值类型、方法名、形参等）

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200724104004.JPG)



## 简单的Person类

```java
package com.yuanbaoqiang.exer;

public class Test {
    public static void main(String[] args){
        Person p1 = new Person();

        p1.name = "Tom";
        p1.age = 18;
        p1.sex = 1;

        p1.study();
        p1.showAge();

        int newAge = p1.addAge(2);
        System.out.println(p1.name + "的新年龄为：" + newAge);

        System.out.println(p1.age); // 20

        //******************************

        Person p2 = new Person();
        p2.showAge(); // 0

    }

}

class Person {
    // 属性
    String name;
    int age;

    /*
    * sex: 1 表明是男性
    * sex: 0 表明是女性
    * */
    int sex;

    public void study() {
        System.out.println("studying");
    }
    public void showAge(){
        System.out.println("age：" + age);
    }

    public int addAge(int i){
        age +=2;
        return age;
    }

}
```

# 对象

## 对象的内存解析

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200724111453.png)



## 对象数组的内存解析

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200724113411.png)



## 练习

> 定义类Student1,包含三个属性：学号number（int），年级state（int），成绩score（int）创建20个学生对象，学号1到20，年级和成绩都由随机数确定。
>
> 1. 问题一：打印出3年纪（state值为3）的学生信息
> 2. 问题二：使用冒泡顺序按照学生成绩排序，并遍历所有学生信息

可将一些功能进行封装成方法，优化代码结构。

```java
/**
 * <h3>我的代码</h3>
 * <p>这是对象数组的练习</p>
 *
 * @author : YuanbaoQiang
 * @date : 2020-07-24 08:59
 **/


package com.yuanbaoqiang.exer;

public class StudentAgain {
    public static void main(String[] args){

        // 创建20个学生信息
        Student1[] s1 = new Student1[20];


        for (int i = 0; i < s1.length; i++) {

            // 创建对象
            s1[i] = new Student1();

            // 分配学生编号
            s1[i].number = i + 1;

            // 分配年级
            // [1,6]
            s1[i].state = (int)(Math.random() * (6 - 1 + 1) + 1);

            // 分配成绩
            // [0,100]
            s1[i].score = (int)(Math.random() * (100 - 0 + 1) + 0);

        }

        StudentAgain sa = new StudentAgain();

        // 遍历学生
        sa.Print(s1);
        System.out.println("===========================================");

        // 问题一：打印出3年纪（state值为3）的学生信息
        sa.searchState(s1,3);
        System.out.println("===========================================");

        // 问题二：使用冒泡顺序按照学生成绩排序，并遍历所有学生信息
        sa.sort(s1);
        sa.Print(s1);

    }

    /**
     * @description: 遍历学生信息
     * @author: YuanbaoQiang
     * @date: 2020/7/24 9:23
     * @param s1 学生数组
     * @return: void
     */
    public void Print(Student1[] s1){
        for (int i = 0; i < s1.length; i++) {
            System.out.println(s1[i].info());
        }
    }

    /**
     * @description: 打印指定年级学生的信息
     * @author: YuanbaoQiang
     * @date: 2020/7/24 9:51
     * @param s1 学生数组
     * @param state 需要筛选的年级
     * @return: void
     */
    public void searchState(Student1[] s1, int state){
        for (int i = 0; i < s1.length; i++) {
            if(s1[i].state == 3){
                System.out.println(s1[i].info());
            }
        }
    }

    /**
     * @description: 冒泡排序学生成绩（从小到大）
     * @author: YuanbaoQiang
     * @date: 2020/7/24 9:58
     * @param s1 需要排序的学生数组
     * @return: void
     */
    public void sort(Student1[] s1){
        for (int i = 0; i < s1.length - 1; i++) {
            for (int j = 0; j < s1.length - 1 -i; j++) {
                if(s1[j+1].score < s1[j].score){
                    Student1 temp;
                    temp = s1[j];
                    s1[j] = s1[j+1];
                    s1[j+1] = temp;
                }
            }
        }
    }

}

class Student1{
    int number, state, score; // 编号，年级，分数

    public String info(){
        return "编号为 " + number + " 的学生" + ",年级为 " + state + ",分数为 " + score;
    }
}

```

