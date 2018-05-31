---
layout:       post
title:        "面试时遇到的一些基础问题"
subtitle:     "《JavaScript高级程序设计》"
date:         2018-04-25 13:00:00
author:       "Raquel"
header-img:   "img/post-bg-2015.jpg"
header-mask:  0.3
catalog:      true
tags:
    - 基础
---
##### JS
###### 1.var let const
使用var声明的变量，其作用域为该语句所在的函数内，且存在变量提升现象；
使用let声明的变量，其作用域为该语句所在的代码块内，不存在变量提升；
使用const声明的是常量，在后面出现的代码中不能再修改该常量的值。

块级作用域：任何一对花括号{}中的语句集都属于一个块，在这之中定义的所有变量在代码块外都是不可见的，我们称之为块级作用域。
函数作用域：定义在函数中的参数和变量在函数外部是不可见的。
注意 for if

###### 2.this
![原文链接](http://www.ruanyifeng.com/blog/2010/04/using_this_keyword_in_javascript.html)
![this的文章链接](/_posts/2018-04-16-this.markdown)

###### 3.通联面试
深拷贝 浅拷贝

寻找数组里面第三大的数

['a','b',['h',['l','g']]] 寻找热词

事件冒泡

垃圾处理

###### 4.vue 路由
HomePage 有多个 div 版面，刷新时，div 状态改变，没办法仍然定位在当前版面
解决：改 div 为嵌套路由
再次出现问题：created 中定义了HomePage 的路由跳转，因为刷新时调用 created，所以路由定位到了第一次进入 HomePage 时的地方，而不是刷新前点击的子路由位置
解决：mounted，在 mounted 中给 defaultActiveIndex 赋值，created 中获取 defaultActiveIndex，然后进行路由跳转
