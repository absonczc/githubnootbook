---
title: Components的v-bind:is
date: 2020-05-13 09:38:11
categories: 
    - 面试题
tags: 
    - VUE
mp3:
cover: https://pic1.zhimg.com/v2-2ad93fccf9862fe5dff82f5c7eabf82e_r.jpg
---

## 情景

最近，收到朋友们去面试的题目，感觉到这道题还挺有意思的。也就记录一下。

给出一个数组对象

``` javascript
var data = [
  {
    name:"jack",
    type:"string"
  },
  {
    name:"james",
    type:"datetime"
  },
  {
    name:"simple",
    type:"datetime"
  },
  {
    name:"kobe",
    type:"int"
  },
  {
    name:"jordan",
    type:"bool"
  },
]
```

根据type的不同,加载不同的组件，譬如 为`string` 的时候加载普通文本框组件，`datetime`加载显示日期选择框组件，`int`加载显示数字框组件，`bool`加载单选框组件。

#### 整个页面不需要v-if,v-else,v-show,switch。用v-if这样的解决方案 百分之九十的人都会做。 在于如果解决If else过多的问题。

## 我用的是 components 的v-bind:is 来完成

``` javascript
<template>
  <component v-for="item in  demo_data" :key="item" v-bind:is="item.type" />
</template>
```

``` javascript
import string from '@/components/string';
import datetime from '@/components/datetime';
import int from '@/components/int';
import bool from '@/components/bool';
export default {
  components: { string,datetime,int,bool },
  data() {
    return {
      demo_data:[
        {
          name:"jack",
          type:"string"
        },
        {
          name:"james",
          type:"datetime"
        },
        {
          name:"simple",
          type:"datetime"
        },
        {
          name:"kobe",
          type:"int"
        },
        {
          name:"jordan",
          type:"bool"
        },
      ]
    }
  }
}
```

# 结后语

> 其实方法很多种，也可以用 `策略模式` 去完成。毕竟这个设计模式 就是为了解决过多繁琐的if,else。