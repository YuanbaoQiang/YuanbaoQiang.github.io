---
title: Java基础10（封装、构造器）
date: 2020-07-28 07:24:23
tags: Java
categories: Java基础
---

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200728084607.png)

<!--more-->

# 封装性和隐藏性

当我们创建一个类的对象以后，我们可以通过“对象.属性”的方式，对对象的属性进行赋值。但是赋值参数操作要受到属性的数据类型和存储范围的制约（例如年龄要大于0，取款金额要小于存款）。但是在实际情况中，我们往往需要给属性赋值加上额外的限制条件。这个条件就不能在属性声明时体现，我们只能通过方法进行限制条件的添加。（比如setlegs()），同时我们需要避免用户再使用“对象.属性”的方式对属性进行赋值，则需要将属性声明为私有的(private)，此时，针对属性就体现了<font color=orange>封装性</font>，此外提供公共的（public）方法来设置（<font color=orange>setXxx()</font>）和获取（<font color=orange>getXxx()</font>）此属性的值。

```java
class Animal{
    String name;
    private int age;
    private int legs; // 腿的个数

    // 提供关于属性age的set和get方法
    public int getAge(){
        return age;
    }

    public void setAge(int a){

    }


    // 对于属性的设置
    public void setLegs(int l){
        if(l >= 0 && l % 2 == 0){
            legs = l;
        }else{
            legs = 0;
            // 抛出一个异常（暂时未讲）
        }
    }

    // 对于属性的获取
    public int getLegs(){
        return legs;
    }


    public void eat(){
        System.out.println("动物进食");
    }

    public void show(){
        System.out.println("name = " + name + ", age = " + age + ", legs = " + legs);
    }
}
```

## 权限修饰符

4种权限修饰符（从小到大排列）：private < default(缺省) < protected < public 

4种权限可以用来修饰类及类的内部结构：<font color=orange>属性</font>、<font color=orange>方法</font>、<font color=orange>构造器</font>、<font color=orange>内部类</font>。

但是修饰类，只可以用：缺省、public。

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200728075442.png)

# 构造器

构造器的作用：创建对象；初始化对象的属性

> 如果没有显示的定义类的构造器的话，则系统默认提供一个空参的构造器
>
> 定义构造器的格式：<font color=orange>权限修饰符  类名（形参列表）{}</font>
>
> 一个类中定义的多个构造器，彼此构成重载
>
> 一旦我们显示的定义了类的构造器之后，系统就不再提供默认的空参构造器
>
> 一个类中，至少会有一个构造器。

```java
public class PersonTest {
    public static void main(String[] args) {
        // 创建类的对象： new + 构造器
        Person p = new Person();
        p.eat();

        Person p1 = new Person("Tom");
        System.out.println("p1的名字是：" + p1.name);

    }
}

class Person{
    // 属性
    String name;
    int age;

    // 构造器
    public Person(){
        System.out.println("com.yuanbaoqiang.java1.Person()...");
    }

    public Person(String n){
        name = n;
    }

    // 方法
    public void eat(){
        System.out.println("人吃饭");
    }

    public void study(){
        System.out.println("人可以学习");
    }
}
```

# 关键字

## this

> this 可以用来修饰：属性、方法、构造器.

### this 修饰属性和方法

在类的方法中，我们可以使用"this.属性" 或 "this.方法" 的方式，调用当前对象属性或方法。但是，通常情况下，我们都选择省略 "this."。特殊情况下，如果方法的形参和类的属性同名时，我们必须显式地使用 "this.变量" 的方式，表明此变量是属性，而非形参。


在类的构造器中，我们可以使用"this.属性" 或 "this.方法" 的方式，调用当前对象属性或方法。但是，通常情况下，我们都选择省略 "this."。特殊情况下，如果构造器的形参和类的属性同名时，我们必须显式地使用 "this.变量" 的方式，表明此变量是属性，而非形参。

```java
public void setName(String name){ // 形参和属性重名
    this.name = name; //如果写 name = name，系统将无法识别，哪个是属性，哪个是输入形参
}// 加上this，代表属于当前对象

public String getName(){
    return name;
}
```

### this修饰构造器

this可以作为一个类中构造器相互调用的特殊格式

```java
class Person{ // 定义Person类
    private String name;
    private int age;

    public Person(){ // 无参数构造器
        this.eat();
        String info = "Person初始化，需要考虑如下的1，2，3，4...（共40行代码）";
        System.out.println(info);
    }

    public Person(int age){
        this(); // 调用本类中无参的构造器
    }

    public Person(String name, int age){
        this(age); // 调用带有一个参数的构造器
        // this.name = name;
        this.age = age;
    }
}
```

## package

package语句作为Java源文件的第一条语句，指明该文件中定义的类所在的包。（若缺省该语句，则指定为无名包）。格式为：<font color = blue>package 顶层包名.子包名;</font>

```java
package com.yuanbaoqiang.java2;
```

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200728083902.png)

## improt

> 1. 在源文件中显式的使用import结构导入指定包下的类、接口；
> 2. 声明在包的声明和类的声明之间；
> 3. 如果需要导入多个结构，则并列写出即可；
> 4. 可以使用“xxx.*”的方式，表示可以导入xxx包下的所有结构；
> 5. 如果使用的类或者接口是java.lang包下定义的，则可以省略import结构；
> 6. 如果使用的类或接口是本包下定义的，则可以省略import结构；
> 7. 如果在源文件中，使用了不同包下的同名的类，则必须至少有一个类需要以全类名的显示；
> 8. import static组合的使用：调用指定类或接口下的静态的属性或方法。