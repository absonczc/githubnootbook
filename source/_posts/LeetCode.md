---
layout: '[posts]'
title: LeetCode
date: 2020-09-16 15:17:04
tags:
---

## 题一：
在一个给定的数组nums中，总是存在一个最大元素 。

查找数组中的最大元素是否至少是数组中每个其他数字的两倍。

如果是，则返回最大元素的索引，否则返回-1。

#### 示例

``` cmd
    输入: nums = [3, 6, 1, 0]
    输出: 1
    解释: 6是最大的整数, 对于数组中的其他整数,
    6大于数组中其他元素的两倍。6的索引是1, 所以我们返回1.

    输入: nums = [1, 2, 3, 4]
    输出: -1
    解释: 3的两倍 大于 4 ，所以我们返回-1
```

#### 解题思路

1. 把数组中最大的 和 第二大的 拿出来比较即可

``` javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var dominantIndex = function(nums) {
    // 找出最大的 ES6的方法 max
    var MaxStr = Math.max(...nums);
    // 把最大的数 从数组去掉 从而继续找 第二大的
    var MaxIndex = nums.indexOf(MaxStr);
    nums.splice(MaxIndex,1);
    var SecondMax = Math.max(...nums);
    if(SecondMax * 2 > MaxStr) {
        return MaxIndex
    }
    return -1
};
```


## 题二：
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

``` cmd
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

### 解题思路

1. 把target 分别与数组每一个数字相减 得出来得数字 判断是否存在于数组中

``` javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
   let index = nums.length;
   while(index < 1) {
       var last = nums.pop()    //删除最后一个元素，并返回 删除的数值
       if(nums.indexOf(target - last) > -1) {
           return nums.indexOf(target - last)
       }
       index--;
   }
};
```


## 题三：


给一个 包含 1 ~ n 的数组，找出序列数中没有的数字
```cmd
输入：[0,3,1]
输出: 2
```

## 解题

``` javascript
var missNumber =  function (nums) {
    var i = nums.length;
    var target = nums.reduce((a,b)=>{return a+b});
    var total = (i+1) * i / 2
    return total - target
}
```


## 题四

给定一个非负整数 num，反复将各个位上的数字相加，直到结果为一位数。

``` cmd
示例:
输入: 38
输出: 2 
解释: 各位相加的过程为：3 + 8 = 11, 1 + 1 = 2。 由于 2 是一位数，所以返回 2。
```