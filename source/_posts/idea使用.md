---
title: IDEA使用（持续更新...）
date: 2020-07-28 08:46:56
tags: Software
categories: IntelliJ IDEA
---

<img src="https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200728090806.png" style="zoom: 33%;" />

<!--more-->

# 注释类设置

## 普通文本注释

注释单行：`//` 

注释多行：`ctrl+shift+/`

## 类注释

左上角选择 File -> Settings -> Editor -> File and Code Templates，

选择Files -> Class，在类声明上填入以下内容，并勾选Enable Live Templates 开启此模板

```java
/**
* <h3>${PROJECT_NAME}</h3>
* <p>${description}</p>
* @author : yourName
* @date : ${YEAR}-${MONTH}-${DAY} ${HOUR}:${MINUTE}
**/
```

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200728090002.png)



## 方法注释

具体细节参考：[idea 自动添加注释 (方法+类 带参数/返回值)](https://www.cnblogs.com/nvsky/p/11199841.html)

效果如下：

![方法注释-范例](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200728090512.png)

# 快捷键

## 循环

在方法内部输入`10.for`回车，即可得到次数为10次的for循环代码。

```java
for (int i = 0; i < 10; i++) {
    
}
```

## 修改变量名

选中需要修改的变量名，然后`shift + f6`批量修改同名变量

## 直接换行

`shift+enter`直接换行



## 类中生成构造器、setter、getter等...

右击，选择generate（生成），选择想要的功能，快捷输入

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200728085239.png)