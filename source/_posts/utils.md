---
title: javascript工具函数
categories:
  - 工具函数
tags:
  - javascript
date: 2020-05-14 17:23:20
mp3:
cover: https://user-gold-cdn.xitu.io/2020/1/16/16fad48d272fc2f9?imageslim
---

## 寻找数组对象中某一个元素相对应的下标

> 找出list2 在 list 的对应下标

``` javascript
var list = [
  {
    name:'apple',
    id:0
  },
  {
    name:'xiaomi',
    id:1
  },
  {
    name:'huawei',
    id:2
  }
];
var list2 = [
  {
    name:'xiaomi',
    id:1
  }
]
```

``` javascript
/**
  * 查找数组想要元素取出下标
  * @param arr
  * @param val
  * @returns {number}
*/
var arr_search = function(arr,val,attr) {
  for(let i = 0; i < arr.length; i++){
    if(arr[i][attr] == val) return i
  }
return -1;
}
var index = arr_search(list,list2[0].id,'id');
console.log(index) // 1
```

## 多维数组，扁平化+去重+排序（多个方式）

> 已知数组 var list = [[1, 2, 2], [3, 4, 5, 5], [6, 7, 8, 9, [11, 12, [12, 13, [14] ] ] ], 10];
> 编写一个程序将数组扁平化去并除其中重复部分数据，最终得到一个升序且不重复的数组

``` javascript
/**
  * 多维数组扁平，排序，去重
*/
var list = [[1, 2, 2], [3, 4, 5, 5], [6, 7, 8, 9, [11, 12, [12, 13, [14] ] ] ], 10];
// 扁平化
// flat(index) index:需要展开的阵列数 [ [...],[[...]] ] 这样为2个
var flatArr = list.flat(4);

// or es6 扩展运算符
// isArray() 方法用于判断一个对象是否为数组。
// .contact() 把数组拼接起来
while (list.some(Array.isArray)) {
list = [].concat(...list);
}

// or 递归
```
