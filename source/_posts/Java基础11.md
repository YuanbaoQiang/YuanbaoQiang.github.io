---
title: Java基础11（继承、多态）
date: 2020-07-30 20:23:48
tags: Java
category: Java基础
---

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200730213721.png)

<!--more-->

# 继承（inheritance）

继承的基本思想是，可以基于已知的类创建新的类。继承已经存在的类就是复用（继承）这些类的方法，同时也可以增加一些新的方法和字段，使得新类能够适应新类的情况。

> 被继承方：超类(superclass)，基类(baseclass)，父类(parent class)
>
> 继承方：子类(subclass)，派生类(derived class)，孩子类(child class)

## 定义子类

用关键字`extends`进行继承操作，存在继承者和被继承者是`is-a`的关系，通常子类会拥有比超类更多的功能！

```java
public class Student extends Person{
    // added methods and fiels
    private String major;
    ...
}
```

## 重写或者覆盖(override)方法

### super

> 1. super可以调用超类中的属性和方法（"super.属性"，"super.方法"）
> 2. 当子类和父类存在同名的属性时，必须显式使用"super.属性"调用超类的属性
> 3. 存在override时，调用父类方法，必须用super关键字

`super`和`this`<font color = orange>并不是类似的概念</font>，`super`并不能像`this`一样作为对象的引用，将值赋予给另一个对象变量，它只是一个指示编译器调用超类方法的特殊关键字。

## 子类构造器

> 1. 在子类的构造器中显式子的使用"super(形参列表)"的方式，调用父类中声明的构造器；
> 2. "super(形参列表)"，必须声明在子类构造器的首行！
> 3. 在类的构造器中，争对"this(形参列表)"或"super(形参列表)"只能二选一，不能同时出现;
> 4. 在类的构造器中，争对"针对this(形参列表)" 或者 "super(形参列表)"，则默认调用父类中空参的构造器：super();
> 5. 在类的多个构造器中，至少有一个类的构造器中使用了"super(形参列表)"，调用父类中的构造器.

子类的构造器不能够访问超类的私有字段，所以必须通过构造一个构造器来初始化这些私有字段。如果子类无显式的调用超类的构造器，则系统默认调用超类的无参数构造器。但是如果超类中无定义一个空参构造器。子类中无显式调用父类中的其它构造器，则编译器报错！

# 多态（polymorphism）

多态使用的前提：要有继承关系，要有方法的重写

`is-a`原则的另一种表述：替换原则（substitution principle），例如可以将子类对象赋予给超类变量，子类的么一个对象也是超类的对象:

```java
Employee e;
e = new employee(...);
e = new Manager(...);
```

```java
Manager boss = new Manager(...);
Employee[] staff = new Employee[3];
Staff[0] = boss;
```

变量stuff[0]和boss引用同一个对象，但是编译器只将stuff[0]看成是一个Employee对象，

<font color =orange>调用的是超类中的方法或者子类中重写的方法！！！！！！！！！</font>