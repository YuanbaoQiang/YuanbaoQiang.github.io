---
title: Java基础03（流程控制语句）
date: 2020-07-18 21:01:53
tags: Java
categories: Java基础
---

![](Java基础03/Java基础03.png)

<!--more-->

# 顺序结构

```java
public static void main(String[] args){
    //顺序执行，根据编写的顺序，从上到下运行
    System.out.println(1);
    System.out.println(2);
    System.out.println(3);
}
```

# 判断语句

格式对就行

> 指定考试成绩，判断学生等级
>
> - 90-100 优秀
> - 80-89 好
> - 70-79 良
> - 60-69 及格
> - 60以下 不及格

```java
// 判断语句
public class Demon02If{
    public static void main(String[] args){
        int score = 60;
        if(score>=90 && score<=100){
            System.out.println("你的成绩属于优秀");
        }else if(score>=80 && score<90){
            System.out.println("你的成绩属于好");
        }else if(score>=70 && score<80){
            System.out.println("你的成绩属于良");
        }else if(score>=60 && score<70){
            System.out.println("你的成绩属于及格");
        }else if(score>=0 && score<60){
            System.out.println("你的成绩属于不及格");
        }else{
            System.out.println("数据错误");
        }
    }
}
```

# 选择语句

## 注意事项

1. 多个case后面的数值不可以重复
2. switch后面小括号当中只能是以下数据类型
3. switch语句可以很灵活，前后顺序可以颠倒，而且break语句可以省略，但是<font color=orange>会一直向下执行，直到有break语句或者整体结束为止</font>

Switch语句的表达式可以是以下几种类型

1. 基本数据类型：byte/short/char/int
2. 引用数据类型：String字符串、enum枚举

```java
public class Demon03Switch{
    public static void main(String[] args){
        int num = 1;
        switch (num){
            case 1:
                System.out.println("星期一");
                break;
            case 2:
                System.out.println("星期二");
                break;
            case 3:
                System.out.println("星期三");
                break;
            case 4:
                System.out.println("星期四");
                break;
            case 5:
                System.out.println("星期五");
                break;
            case 6:
                System.out.println("星期六");
                break;
            case 7:
                System.out.println("星期日");
                break;
            default:
                System.out.println("数据不合理");
                break; 

        }
    }
}
```

一般default后的break也要书写，并且case如果没有break关键字，会向下继续执行

```java
public class Demon03Switch{
    public static void main(String[] args){
        int num = 1;
        switch (num){
            case 1:
                System.out.println("星期一");
                // break;
            case 2:
                System.out.println("星期二");
                break;
            case 3:
                System.out.println("星期二");
                break;
            default:
                System.out.println("数据不合理");
                break; 
```

此时输出为

```bash
星期一
星期二
```

# 循环语句

主要有for, while, do-while三种循环，格式对就行。

```java
// 求出1-100之间的偶数和
public class Demon07Test{
    public static void main(String[] args){
        int count = 0;
        int num = 0;
        int j = 1;
        for(int i=1; i<=100; i++){
            if(i%2==0){
                count = count + i;
            }
            num++;
        }

        // while 方法
         /*while(j<=100){
            if(j%2==0){
                count = count + j;
            }
            j++;
            num++;
        }*/

        // do-while方法
         /*do{
            if(j%2==0){
                count =count + j;
            }
            j++;
            num++;

        }while(j<=100);*/

        System.out.println(num+" "+count);
    }

}
```

## 注意事项

1. 如果条件判断从来没有满足过，那个for和while循环将会执行0次，但是do-while循环至少一次
2. for循环的变量在小括号当中定义，只有循环内部才可以使用，while和do-while循环初始化语句本来就在外面，所以出来循环之后还可以继续使用

```java

public class Demon08LoopDifference{
    public static void main(String[] args){
        for(int i = 1; i < 0; i++){
            System.out.println("HelloWorld");
        }
        // System.out.println(i);  这一行是错误写法！因为变量i定义在for循环内，只有for循环内可用
        System.out.println("========================");

        int i = 1;
        do{
            System.out.println("World");
            i++;
        }while(i<=10);

        //现在已经退出循环了，我们仍然可以使用变量i
        System.out.println(i);

    }
}
```

# 死循环

就是在true的环境一直运行

```java
/*
 * 死循环
 * 死循环的标准格式：
 * while(true){
 *   循环体
 * }
 *
 * */

public class Demon11DeapLoop{
    public static void main(String[] args){
        while(true){
            System.out.println("I Love Java");
        }
        // System.out.println("Hello");
    }
}
```

# 嵌套循环

```java
// 小时--分钟--秒
public class Deomon13LoopHourAndMinute{
    public static void main(String[] args){
        for(int hour = 0; hour < 24; hour++){ // 外层控制小时

            for(int minute = 0; minute < 60; minute++){ // 内层控制小时之内的分钟

                for(int second = 0; second < 60; second++){ // 最内层控制分钟内的秒数
                    System.out.println(hour+"点"+minute+"分"+second+"秒");
                }

            }

        }
    }
}
```