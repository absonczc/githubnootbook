---
title: vue的v-for中index为什么不能:key的值
date: 2020-05-13 11:34:12
categories: 
    - 面试题
tags: 
    - VUE
mp3:
cover: http://desk.fd.zol-img.com.cn/t_s1280x1024/g5/M00/0B/08/ChMkJlxtLuqIXzy4AALlTpmEnAEAAvA_QM7RJYAAuVm014.jpg
---

**[想知道为什么要用key吗？](https://blog.csdn.net/aihuanhuan110/article/details/98223011)**

## 为什么不能用index作为key的值

1. 会影响性能
2. 会发生一些意想不到的状态BUG

举个例子：

``` javascript
<template>
  <div v-for="(item, index) in list" :key="index" >{{item.name}}</div>
</template>
```

``` javascript
const lisy = [
  {
    id:1,
    name:'jone'
  },
  {
    id:2,
    name:'sony'
  },
  {
    id:3,
    name:'xiaomi'
  },
  {
    id:3,
    name:'apple'
  }
]
```

> 此时 如果删除第二个话就会出现问题了

### 删除前

id | index | key | name
:-: | :-: | :-: | :-:
1 | 0 | 0 | jone
2 | 1 | 1 | sony
3 | 2 | 2 | xiaomi
4 | 3 | 3 | apple

### 删除后

id | index | key | name
:-: | :-: | :-: | :-:
1 | 0 | 0 | jone
3 | 1 | 1 | xiaomi
4 | 2 | 2 | apple

这里除了 jone意外 你会发现 xiaomi , apple 的key绑定的关系都会变化了，导致重新渲染，影响性能。

且当选中 xiaomi 的时候吗， sony给删除了的时候。如果用index 作为key 来选中选项的话，这里就会变成 apple 被选中了。就是这一Bug.
