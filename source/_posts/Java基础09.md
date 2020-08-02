---
title: Java基础09（值传递、递归）
date: 2020-07-26 18:41:02
tags: Java
categories: Java基础
---

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200726185140.png)

<!--more-->

# 匿名对象的使用

匿名对象就是没有明确的给出名字的对象，是对象的一种简写形式。一般匿名对象<font color=orange>只能调用一次</font>，而且匿名对象<font color=orange>只在堆内存中开辟空间，而不存在栈内存的引用</font>。

```java
package com.yuanbaoqiang.java;

public class InstanceTest {
    public static void main(String[] args){
       Phone p = new Phone();
       // p = null;
       System.out.println(p); // 地址值

        p.playGame();
        p.sendeMail();

        // 匿名对象
/*        new Phone().sendeMail();
        new Phone().playGame();*/

        new Phone().price = 1999;
        new Phone().getPrice();

        // *******************************************
        PhoneMall mall = new PhoneMall();
        mall.show(new Phone());

    }
}

class PhoneMall{
    public void show(Phone phone){
        phone.sendeMail();
        phone.playGame();
    }
}

class Phone{
    double price; // 价格

    public void sendeMail(){
        System.out.println("发送邮件");
    }

    public void playGame(){
        System.out.println("玩游戏");
    }

    public void getPrice(){
        System.out.println("手机的价格为：" + price);
    }
}
```

# 自定数组的工具类

定义了一个数组工具类`ArrayUtil`：

求<font color=orange>最值，总和，平均数，数组反转，复制，排序，遍历，查找指定元素（线性查找）。</font>

```java
/**
 * <h3>我的代码</h3>
 * <p>自定义数组的工具类</p>
 *
 * @author : YuanbaoQiang
 * @date : 2020-07-26 08:25
 **/

package com.yuanbaoqiang.java;

public class ArrayUtil {

    // 求数组的最大值
    /**
     * @description: 求数组的最大值
     * @author: YuanbaoQiang
     * @date: 2020/7/26 8:38
     * @param arr
     * @return: int
     */
    public int getMax(int[] arr){
        int max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            max = arr[i] > max ? arr[i] : max;
        }
        return max;
    }

    // 求数组的最小值
    /**
     * @description: 求数组的最小值
     * @author: YuanbaoQiang
     * @date: 2020/7/26 8:38
     * @param arr
     * @return: int
     */
    public int getMin(int[] arr){
        int min = arr[0];
        for (int i = 1; i < arr.length; i++) {
            min = arr[i] < min ? arr[i] : min;
        }
        return min;
    }

    // 求数组的总和
    /**
     * @description: 求数组的总和
     * @author: YuanbaoQiang
     * @date: 2020/7/26 8:41
     * @param arr
     * @return: int
     */
    public int getSum(int[] arr){
        int sum= 0;

        for (int i = 0; i < arr.length; i++) {
            sum +=arr[i];
        }
        return sum;
    }

    // 求数组的平均值
    /**
     * @description: 求数组的平均数
     * @author: YuanbaoQiang
     * @date: 2020/7/26 8:50
     * @param arr
     * @return: double
     */
    public double getAve(int[] arr){
        return getSum(arr) / arr.length;
    }


    // 反转数组
    /**
     * @description: 反转数组
     * @author: YuanbaoQiang
     * @date: 2020/7/26 8:53
     * @param arr
     * @return: void
     */
    public void reverse(int[] arr){
        for(int min=0, max=arr.length-1; min < max; min++, max--){
            int temp = arr[min];
            arr[min] = arr[max];
            arr[max] = temp;
        }
    }

    // 复制数组
    /**
     * @description: 复制数组
     * @author: YuanbaoQiang
     * @date: 2020/7/26 18:56
     * @param arr 
     * @return: int[]
     */
    public int[] copy(int[] arr){
        int[] arr1 = new int[arr.length];
        for (int i = 0; i < arr1.length; i++) {
            arr1[i] = arr[i];
        }
        return arr1;
    }

    
    // 数组排序
    /**
     * @description: 冒泡排序
     * @author: YuanbaoQiang
     * @date: 2020/7/26 8:59
     * @param arr
     * @return: void
     */
    public void sort(int[] arr){
        for (int i = 0; i < arr.length - 1; i++) {
            for (int j = 0; j < arr.length - 1 -i; j++) {
                if(arr[j] > arr[j+1]){
                    int temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
        }
    }

    // 遍历数组
    /**
     * @description: 遍历数组
     * @author: YuanbaoQiang
     * @date: 2020/7/26 18:56
     * @param arr 
     * @return: void
     */
    public void print(int[] arr){
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i]+" ");
        }
    }

    // 查找指定元素
    /**
     * @description: 查找指定元素
     * @author: YuanbaoQiang
     * @date: 2020/7/26 9:07
     * @param arr
     * @param dest
     * @return: int
     */
    public int getIndex(int[] arr, int dest){
        // 线性查找
        for (int i = 0; i < arr.length; i++) {
            if(dest == arr[i]){
                return  i;
            }
        }
        return -1; // 返回一个负数，表示没有找到
    }
}
```

# 可变个数形参的方法

> 1. 可变个数形参的格式： <font color=orange>数据类型 ... 变量名</font>
> 2. 当调用可变个数形参的方法时，传入的参数个数可以是0个，1个，2个，或者多个
> 3. 可变形参的方法与本类中方法名相同，形参不同的方法之间构成重载
> 4. 可变个数形参的方法与本类中方法名相同，形参类型也相同的数组之间不构成重载。换句话说，二者不能共存
> 5. 可变个数形参在方法的形参中，<font color=orange>必须声明在末尾</font>
> 6. 可变个数形参在方法的形参中，最多只能声明一个可变形参

String ... strs相比于String[] strs更简单，使用前不需要new一个数组，直接写入实参即可。

```java
/**
 * <h3>我的代码</h3>
 * <p>可变个数形参的方法</p>
 *
 * @author : YuanbaoQiang
 * @date : 2020-07-26 10:11
 **/

package com.yuanbaoqiang.java1;


public class MethodArgsTest {

    public static void main(String[] args){
        MethodArgsTest test = new MethodArgsTest();
        // test.show(12);
        test.show("AA", "CC", "BB", "DD");

    }

    public void show(int i){

    }

    public void show(String s){
        System.out.println("show(String s)");
    }

    /**
     * @description: 可变个数形参的方法
     * @author: YuanbaoQiang
     * @date: 2020/7/26 10:45
     * @param strs
     * @return: void
     */
    public void show(String ... strs){
        System.out.println("show(String ... strs)");
        for(int i = 0; i < strs.length; i++){
            System.out.println(strs[i]);
        }
    }


/*    public void show(String[] strs){

    }*/

    public void show(int i, String ... strs){

    }

}
```

# 值传递机制

> 形参：方法定义时，声明的小括号内的参数
>
> 实参：调用方法时，实际传递给形参的数据

```java
public class ValueTransferTest1 {
    public static void main(String[] args){
        // 交换两个变量的值得操作
        int m = 10;
        int n = 20;
        System.out.println("m = " + m + ", n = " + n);

        // 交换两个变量得值得操作
/*        int temp = m;
        m = n;
        n = temp;*/

        ValueTransferTest1 test = new ValueTransferTest1();
        test.swap(m, n);
        System.out.println("m = " + m + ", n = " + n);

    }

    public void swap(int m, int n){
        int temp = m;
        m = n;
        n = temp;
    }
}
```

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200726213053.jpg)



![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200726213212.jpg)



![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200726213138.jpg)

# 递归方法

传送门：[递归](https://yuanbaoqiang.github.io/2020/07/26/递归/#more)。