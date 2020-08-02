---
title: Java基础12（包装类、static、代码块）
date: 2020-08-01 20:15:19
tags: Java
category: Java基础
---

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200801201624.png)

<!--more-->

# Object

Object类是Java中所有类的始祖，Java中每个类都扩展了Object，但是不需要写`extends`。

# 方法重写

## equals()

> 1. 是一个方法，而非运算符；
> 2. 只能适用于引用数据类型；
> 3. 像String、Date、File、包装类等都重写了Object类中的equals()方法；
> 4. 通常情况下，我们自定义的类如果使用equals()的话，也通常是比较两个对象的"实体内容"是否相同，那么，我们就需要对Object类中的equals()进行重写。

Object类中equals()的定义：

```java
public boolean equals(Object obj){
    return (this == obj);
}
```

Object类中定义的equals()和==的作用是相同的：比较两个对象的地址值是否相同，即两个引用。

**比较两个对象的实体内容，重写：**

```java
//重写的原则：比较两个对象的实体内容(即：name和age)是否相同
	//手动实现equals()的重写
	@Override
	public boolean equals(Object obj) {

		System.out.println("Customer equals()....");
		if (this == obj) {
            return true;
        }

		if(obj instanceof Customer){
			Customer cust = (Customer)obj;
			//比较两个对象的每个属性是否都相同
			if(this.age == cust.age && this.name.equals(cust.name)){
				return true;
			}else{
				return false;
			}

			//或
			return this.age == cust.age && this.name.equals(cust.name);
		}else{
			return false;

		}

	}
```

## toString()

> 1. 当我们输出一个对象的引用时，实际上就是调用当前对象的toString();
> 2. 像String、Date、File、包装类等都重写了Object类中的toString()方法。使得在调用对象的toString()时，返回"实体内容"信息;
> 3. 自定义类也可以重写toString()方法，当调用此方法时，返回对象的"实体内容".

Object类中toString()的定义：

```java
public String toString() {
    return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

**输出两个对象的实体内容，重写：**

```java
@Override
public String toString() {
    return "Customer [name=" + name + ", age=" + age + "]";
}
```

# 包装类

针对八种数据类型定义相应的引用类型-包装类（封装类）

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200801210425.png)

## 基本数据类型与包装类的相互转换

### 基本数据类型-->包装类

#### 调用包的构造器

```java
// 基本数据类型-->包装类：调用包装类的构造器
    @Test
    public void test1(){
        int num1 = 10;

        Integer in1 = new Integer(num1);
        System.out.println(in1.toString());

        Integer in2 = new Integer("123");
        System.out.println(in2.toString());

        // 报异常
/*        Integer in3 = new Integer("123abc");
        System.out.println(in3.toString());*/

        Float f1 =  new Float(12.3f);
        Float f2 = new Float("12.3");
        System.out.println(f1);
        System.out.println(f2);

        Boolean b1 = new Boolean(true);
        Boolean b2 = new Boolean("T");
        Boolean b3 = new Boolean("true123");
        System.out.println(b3);
    }
```

### 包装类-->基本数据类型

#### 调用包装类的的xxxValue()方法

```java
//包装类-->基本数据类型：调用包装类的xxxValue()
@Test
public void test2(){
    Integer in1 = new Integer(12);

    int i1 = in1.intValue();
    System.out.println(i1 + 1);


    Float f1 = new Float(12.3);
    float f2 = f1.floatValue();
    System.out.println(f2 + 1);
}
```

### 自动拆箱和自动装箱

#### 自动装箱

```java
// 自动装箱： 基本数据类型 -- > 包装类
int num2 =10;
Integer in1 = num2; // 自动装箱

boolean b1 = true;
Boolean b2 = b1; // 自动装箱
```

#### 自动拆箱

```java
// 自动拆箱： 包装类-->基本数据类型
System.out.println(in1.toString());

int num3 = in1; // 自动拆箱
```

## 包装类与String的相互转换

### 连接运算

### String重载的valueOf()方法

```java
// 基本数据类型、包装类-->String类：调用String重载的valueOf(Xxxx xxx)
@Test
public void test4(){
    int num1 = 10;
    //方式1：连接运算
    String str1 = num1 + "";
    System.out.println(str1);
    // 方式2：调用String重载的valueOf(Xxxx xxx)
    float f1 = 12.3f;
    String str2 = String.valueOf(f1); // "12.3"
    System.out.println(str2);

    Double d1 = new Double(12.4);
    String str3 = String.valueOf(d1);
    System.out.println(str3);

}
```

# 关键字

## instanceof

`instanceof` 是 Java 的保留关键字。它的作用是测试它左边的对象是否是它右边的类的实例，返回 boolean 的数据类型。

## static

static可以用来修饰类的结构：属性、方法、代码块、内部类

### static修饰属性：静态变量（或类变量）

**实例变量**：我们创建了类的多个对象，每个对象都独立的拥有一套类中的非静态属性，当修改其中一个对象中的非静态属性时，不会导致其他对象中同样的属性值的修改。

**静态变量**：我们创建了类的多个对象，多个对象共享同一个静态变量。当通过某一个对象修改静态变量时，会导致其他对象调用此静态变量时，是修改过了的。

|      | 静态变量 | 实例变量 |
| ---- | -------- | -------- |
| 类   | yes      | no       |
| 对象 | yes      | yes      |

### static修饰方法

静态方法中，只能调用静态的方法或属性。

非静态方法中，既可以调用非静态的方法或属性，也可以调用静态的方法或属性。

|      | 静态方法 | 非静态方法 |
| ---- | -------- | ---------- |
| 类   | yes      | no         |
| 对象 | yes      | yes        |



### 类变量 VS 实例变量 内存解析

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200801212055.jpg)

### 其他说明

**static修饰属性的其他说明：**

> 1. 静态变量随着类的加载而加载。 可以通过"类.静态变量"的方式进行调用；
> 2. 静态变量的加载要早于对象的创建；
> 3. 由于类只会加载一次，则静态变量在内存中也只会存在一份：存在方法区的静态域中。

**static修饰方法的其他说明：**

> 1. 静态方法中，只能调用静态的方法或属性；
> 2. 非静态方法中，既可以调用非静态的方法或属性，也可以调用静态的方法或属性。

## final

**final可以修饰的结构：类、方法、变量**

> 1. final用来修饰一个类: 此类不能被其他类继承，比如：String类、System类、StringBuffer类；
> 2. final用来修饰方法：表明此方法不可以被重写，比如：Object类中getclass()；
> 3. final用来修饰变量：此时的"变量"就称为是一个常量

**final修饰属性：可以考虑值得位置有：显式初始化、代码块中初始化、构造器中初始化**

### 显示初始化

```java
final int WIDTH = 0;
```

### 代码块初始化

```java
final int LEFT;
{
	LEFT = 1;
}
```

### 构造器初始化

```java
final int RIGHT;
public FinalTest(){
    RIGHT = 20;
}
```

调用show方法后，num即不可更改。

```java
public void show(final int num){
    // num++; 报错
    System.out.println(num);
}
```

# 设计模式（单例）

## 饿汉式

> 1. 私有化类的构造器；
> 2. 内部创建类的对象；
> 3. 提供公共的方法，返回类的对象；
> 4. 要求此对象也必须是静态的。

**坏处：**对象加载时间过长

**好处：**饿汉式是线程安全的

```java
public class SingletonTest1 {
    public static void main(String[] args) {
        
        Bank bank1 = Bank.getInstance();
        Bank bank2 = Bank.getInstance();
        System.out.println(bank1 == bank2);
        
    }
}


class Bank{

    // 1. 私有化类的构造器
    private Bank(){

    }

    // 2. 内部创建类的对象
    // 4. 要求此对象也必须是静态的
    private static Bank instance = new Bank();

    // 3. 提供公共的方法，返回类的对象
    public static Bank getInstance(){
        return instance;
    }

}
```

## 懒汉式

> 1. 私有化类的构造器；
> 2. 声明类的对象，没有初始化
> 3. 提供公共的方法，返回类的对象；
> 4. 要求此对象也必须是静态的。

**好处：**延迟对象的创建。

**坏处：**以下写法线程不安全（后续修改！！！）

```java
package com.yuanbaoqiang.exer;

public class SingletonTest2 {
    public static void main(String[] args) {
        Order order1 = Order.getInstance();
        Order order2 = Order.getInstance();
        System.out.println(order1 == order2);

    }
}
class Order{

    // 1. 私有化类的构造器
    private Order(){

    }

    // 2. 声明当前类的对象，没有初始化
    // 4. 此对象也必须声明为static的
    private  static Order instance = null;

    // 3. 声明public、static的返回当前类对象的方法
    public static Order getInstance(){
        if(instance == null){
            instance = new Order();
        }
        return instance;
    }

}
```

# 代码块

## 静态（static）

> 1. 内部可以有输出语句；
> 2. 随着类的加载而执行，而且只加载一次；
> 3. 如果一个类中定义了多个静态代码块，则按照声明的先后顺序执行

## 非静态

> 1. 内部可以有输出语句；
> 2. 随着对象的创建而执行；
> 3. 每创建一个对象，就执行一次非静态代码；
> 4. 作用：可以创建对象时，对对象的属性等进行初始化。

# 属性赋值的先后顺序（完结）

1. 默认初始化
2. 显式初始化/ 5 在代码块中赋值
3. 构造器中初始化
4. 有了对象后，通过"对象.属性"或"对象.方法"的方式进行赋值

执行的先后顺序：1 - 2 / 5（取决于代码的书写先后顺序）- 3 - 4