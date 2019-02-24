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

寻找数组里面第三大的数：
```
var thirdMax = function(nums) {
    let first, second, third;
    first = Number.MIN_SAFE_INTEGER;
    second = Number.MIN_SAFE_INTEGER;
    third = Number.MIN_SAFE_INTEGER;
    for(let i = 0; i < nums.length; i +=1) {
        if (nums[i] > first){
            third = second;
            second = first;
            first = nums[i];
        } else if (nums[i] < first && nums[i] > second) {
            third = second;
            second = nums[i];
        } else if (nums[i] < second && nums[i] > third) {
            third = nums[i];
        }
    }
    if (third === Number.MIN_SAFE_INTEGER) {
        return second;
    } else if (second === Number.MIN_SAFE_INTEGER) {
        return first;
    }
    return third;
};

console.log(thirdMax([1,2]));
```

['a','b',['h',['l','g']]] 寻找热词

事件冒泡

垃圾处理

###### 4.vue 路由
HomePage 有多个 div 版面，刷新时，div 状态改变，没办法仍然定位在当前版面
解决：改 div 为嵌套路由
再次出现问题：created 中定义了HomePage 的路由跳转，因为刷新时调用 created，所以路由定位到了第一次进入 HomePage 时的地方，而不是刷新前点击的子路由位置
解决：mounted，在 mounted 中给 defaultActiveIndex 赋值，created 中获取 defaultActiveIndex，然后进行路由跳转

###### 5.vue 生命周期
**created**：在模板渲染成 html 前调用，初始化某些属性值，然后再渲染成视图。
created 可以访问 data 和 computed 里的属性(reactive data 和 events)。但模板和虚拟 DOM 无法访问
**mounted**：在模板渲染成 html 后调用，初始化页面完成后。

Vue 组件的生命周期分为四个阶段：

创建阶段：主要用于组件创建时，获取数据设置组件。
beforeCreate
created：能够访问创建成功的组件实例，但不能访问模板，el 或 DOM

挂载阶段：主要用于访问组件 DOM 。
beforeMount
mounted：能够访问组件模板

更新阶段：数据变化，组件重新渲染。
beforeUpdate：能够访问组件更新后的数据，但无法访问 DOM
updated：能够访问 DOM

销毁阶段：用于销毁组件，做清理工作
beforeDestory：销毁前还能访问组件实例
destory

###### 6.v-model
v-model 无法绑定一个 Object，当直接定义 Object 的时候。需要写成 this.$set(obj, key, value);

###### 7.
typeof null    Object
typeof function    function
typeof [1,2,3]    Object

###### 8.
html 无法解析 \n
解决方法：white-space: pre-line;

###### 9.const 好处
可以把逻辑错误变成运行错误

###### 10.git删除提交历史
```
git filter-branch --force --index-filter 'git rm -rf --cached --ignore-unmatch test/test-projects/projectB' --prune-empty --tag-name-filter cat -- --all
```
```
git push origin --force --all
```
