---
title: Java基础07（简单算法补充，后续继续更新）
date: 2020-07-22 17:47:07
tags: Java
categories: Java基础
---

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200722210826.png)

回形数、快速排序部分:boom:得空补齐~

<!--more-->

# 数组元素的赋值

## 杨辉三角

```java
1  
1  1  
1  2  1  
1  3  3  1  
1  4  6  4  1  
1  5  10  10  5  1  
1  6  15  20  15  6  1  
1  7  21  35  35  21  7  1  
1  8  28  56  70  56  28  8  1  
1  9  36  84  126  126  84  36  9  1
```

> 1. 第一行有 1 个元素，第n行有n个元素
> 2. 每一行的第一个元素和最后一个元素都是1
> 3. 从第三行起，对于非第一个元素和最后一个元素。即：
>
> ```JAVA
> yangHui[i][j] = yangHui[i-1][j-1] + yangHui[i-1][j]
> ```

```java
public class YangHui {
    public static void main(String[] args) {
        // 1. 声明并初始化二维数组
        int[][] yangHui = new int[10][];

        // 2. 给数组的元素赋值
        for (int i = 0; i < yangHui.length; i++) {
            yangHui[i] = new int[i+1]; // 初始化列元素

            // 给首末元素赋值
            yangHui[i][0] = yangHui[i][i] = 1;

            // 给每行的非首末元素赋值
            if(i > 1){
                for(int j = 1; j < yangHui[i].length-1; j++){
                    yangHui[i][j] = yangHui[i-1][j-1] + yangHui[i-1][j];
                }
            }
        }

        // 3. 遍历
        for (int i = 0; i < yangHui.length; i++) {
            for (int j = 0; j < yangHui[i].length; j++) {
                System.out.print(yangHui[i][j] + "  ");
            }
            System.out.println();
        }

    }
}
```

## 回形数 （:facepunch:得空补齐）

# 求整型数组中元素的最值、总和、平均数

> 定义一个 int 型的一维数组，包含 10 个元素， 分别赋一些随机整数个元素，
>
> 然后求出所有元素的最大值， 然后求出所有元素的最大值， 最小值，平均值， 并输出 出来。

随机数采用Math.random()获取

```java
int b=(int)(Math.random()*10);//生成[0,9]之间的随机整数。
int temp = (int)(Math.random() * (n+1-m) + m); //生成从m到n的随机整数[m,n]
```



```java
public class ArrayTest1 {
    public static void main(String[] args) {
        int[] arr = new int[10];
        for (int i = 0; i < arr.length; i++) {
            arr[i] = (int) (Math.random() * (99 - 10 + 1) + 10);
           
        }

        // 遍历
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();

        // 求最大值
        int maxValue = arr[0];
        for (int i = 1; i < arr.length; i++) {
            maxValue = arr[i] > maxValue ? arr[i] : maxValue;
        }
        System.out.println("最大值为：" + maxValue);

        // 求最小值
        int minValue = arr[0];
        for (int i = 1; i < arr.length; i++) {
            minValue = arr[i] < minValue ? arr[i] : minValue;
        }
        System.out.println("最小值为：" + minValue);

        // 求总和
        int sum = 0;
        for (int i = 0; i < arr.length; i++) {
            sum += arr[i];
        }
        System.out.println("总和为：" + sum);


        // 求平均数
        int ave = sum/arr.length;
        System.out.println("平均数为：" + ave);
    }
}
```



# 数组的复制、反转、查找

## 复制

```java
for (int i = 0; i < array2.length; i++) {
    array2[i] = array1[i];
}
```

## 反转

见[Java基础05（数组-单维）]([https://yuanbaoqiang.github.io/2020/07/20/Java%E5%9F%BA%E7%A1%8005/#more](https://yuanbaoqiang.github.io/2020/07/20/Java基础05/#more))

## 查找

### 线性查找

> 按照循环次数依次查找

```java
public class ArraySearch01 {
    public static void main(String[] args) {

        // 查找（或搜索）
        // 线性查找：
        String dest = "BB";
        boolean isFalse = true;

        String[] arr = new String[]{"JJ","DD","MM","BB","GG","CC"};
        for (int i = 0; i < arr.length; i++) {

            if(dest.equals(arr[i])){
                System.out.println("找到了指定的元素，位置为：" + i);
                isFalse = false;
                break;
            }
        }
        if(isFalse){
            System.out.println("很遗憾，没有找到哦！");

        }
    }
}
```

### 二分法

> 前提：所查找的元素必须有序

```java
public class ArraySearch01 {
    public static void main(String[] args) {
        // 二分法查找
        // 前提：所要查找的数组必须有序
        int[] arr2 = new int[]{-98,-34,2,34,54,66,79,105,210,333};
        int dest1 = 334;
        int head = 0; // 初始的首索引
        int end = arr.length-1; // 初始的末索引
        boolean isFalse1 = true;
        while(head <= end){
            int middle = (head + end)/2;
            if(dest1 == arr2[middle]){
                System.out.println("找到了指定的元素，位置为：" + middle);
                isFalse1 = false;
                break;
            }else if(arr2[middle]>dest1){
                end = middle - 1;
            }else{// arr2[middle]<dest1
                head = middle +1;
            }
        }

        if(isFalse1){
            System.out.println("很遗憾 没有找到");
        }

    }
}
```

# 数组元素的排序算法（十个）

可参考：

[十大经典排序算法（动图演示）](https://www.cnblogs.com/onepixel/p/7674659.html)

## 冒泡排序

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200722210943.gif)

```java
import java.util.Arrays;
public class BubbleSort {
    public static void main(String[] args){
        int[] arr = new int[]{34,5,22,-98,6,-76,0,-3};
        System.out.println(Arrays.toString(arr));

        for (int i = 0; i < arr.length-1; i++) {
            for (int j = 0; j < arr.length-1-i; j++) {
                if(arr[j] > arr[j+1]){
                    int temp = arr[j+1];
                    arr[j+1] = arr[j];
                    arr[j] = temp;

                }
            }
        }
        System.out.println(Arrays.toString(arr));       
    }
}
```

## 快速排序（:facepunch:得空补齐）

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200722210956.gif)

# 常见异常

```java
public class ArrayExceptionTest {
    public static void main(String[] args){
        // 1. 数组角标越界的异常：ArrayIndexOutOfBoundsException
        int[] arr = new int[]{1,2,3,4,5};

        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[-2]);
        }

        
        // 2. 空指针异常：NullPointerException

        // 情况一
        int[] arr1 = new int[]{1,2,3};
        arr1 = null;
        System.out.println(arr1[0]);

        // 情况二
        int[][] arr2 = new int[4][];
        System.out.println(arr2[0]); // null
        System.out.println(arr2[0][0]); // 空指针

        // 情况三
        String[] arr3 = new String[]{"AA","BB","CC"};
        arr3[0] = null;
        System.out.println(arr3[0].toString()); // 空指针异常

    }
}
```