---
layout: '[layout]'
title: web前端自测
date: 2020-08-10 10:29:23
tags:
---

# 箭头函数是没有自己的this

如果有引用的```this``` 那么就会指向外部函数：例子：

``` javascript
var obj = {
    name:'lihao',
    say:()=>{
        console.log(`hello ${this.name}`)   // say 的外部函数 是window 
        //  window
    },
    talk() {
        var hello = ()=>{console.log(`hello ${this.name}`)}     // hello 的 外部函数是 talk
        //  lihao
        hello();
    }
}
```

# Vue 关于 父组件周期到 子组件周期 的顺序

父组件：beforecreated() => created() => beforemount() => 子组件: beforecreated() => created() => beforemount() => mounted()

父组件: beforeUpdate() => 子组件(beforeUpdate()) => 子组件(Updated())  => 父组件: Updated()

父组件: beforeDestroy() => 子组件(beforeDestroy()) => 子组件(destroyed())  => 父组件: destroyed()





