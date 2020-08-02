---
title: LeetCode-两数之和（哈希映射）
date: 2020-07-31 08:28:22
tags:
- Algorithm
- 哈希映射
category: LeetCode
mathjax: true
---

![](https://cdn.jsdelivr.net/gh/YuanbaoQiang/PicGoBed/img/20200731084335.jpeg)

<!--more-->

# 题目要求

给定一个整数数组`nums`和一个目标值`target`，请你在该数组中找出和为目标值的那两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

**示例:**

```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

原题链接：[两数之和](https://leetcode-cn.com/problems/two-sum/)

# 解题过程

## 循环

> 空间复杂度：$O(1)$
>
> 时间复杂度：$O(n^2)$

```java
class Solution {
     public int[] twoSum(int[] nums, int target){
         int[] result = new int[2];
         for(int i = 0; i < nums.length; i++){
             for(int j = 0; j < nums.length; j++){
                 if(i < j && nums[i] + nums[j] == target){
                     result[0] = i;
                     result[1] = j;
                 }
             }
         }
         return result;
     }
}
```

## 哈希表

参考：[画解算法：1. 两数之和](https://leetcode-cn.com/problems/two-sum/solution/jie-suan-fa-1-liang-shu-zhi-he-by-guanpengchn/)

1. 遍历数组`nums`，判断map中是否存在`target-num[i]`的key值;
2. 将不满足条件的kay-value存入map中;
3. 继续遍历直到满足条件的数值为止，不满足则返回下标为[-1,-1]的数组。

```java
class Solution {
     public int[] twoSum(int[] nums, int target){
         HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
         for(int i = 0; i < nums.length; i++){
             if(map.containsKey(target-nums[i])){
                 return new int[]{map.get(target-nums[i]),i};
             }
             map.put(nums[i],i);
         }
         return new int[]{-1,-1};
     }
}
```

> 空间复杂度：$O(1)$
>
> 时间复杂度：$O(n)$

