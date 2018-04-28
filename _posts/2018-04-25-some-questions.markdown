---
layout:       post
title:        "面试时遇到的一些基础问题"
subtitle:     "《JavaScript高级程序设计》"
date:         2018-04-11 13:00:00
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

###### 2.this
![原文链接](http://www.ruanyifeng.com/blog/2010/04/using_this_keyword_in_javascript.html)
![this的文章链接](/_posts/2018-04-16-this.markdown)
