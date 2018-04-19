---
layout:       post
title:        "基本概念"
subtitle:     "《JavaScript高级程序设计》"
date:         2018-04-11 13:00:00
author:       "Raquel"
header-img:   "img/post-bg-2015.jpg"
header-mask:  0.3
catalog:      true
tags:
    - 读书笔记
---

### 变量

ECMAScript的变量是松散型，可以保存任何类型的数据。
```
var message = 'hi';
message = 100;
// 有效，但不推荐
```

var 定义的是局部变量，在函数退出后会被销毁，例如：
```
function test() {
  var message = 'hi';
}
test();
alert(message); // 错误
```

省略 var 操作符，会创建一个全局变量
```
function test() {
  message = 'hi';
}
test();
alert(message); // hi
```

### 数据类型

基本数据类型：Undefined、 Null、 Boolean、 Number 和 String。
复杂数据类型：Object。

#### 1.typeof 操作符

```
alert(typeof null); // Object。因为特殊值 null 被认为是一个空的对象引用
```

#### 2.Undefined

```
var message;
alert(message == undefined); // true
```
```
var message = undefined;
alert(message == undefined); // true
```
用 undefined 初始化了 message，但是没必要这么做。

但是，包含 undefined 值得变量与尚未定义的变量还是不一样的。
```
var message;
alert(message); // “undefined”
alert(age); // 错误
```
但是使用 typeof，都会返回 undefined。虽然这两个变量从技术角度看有本质区别，但是逻辑上合理。

#### 3.Null

表示空对象指针。如果定义的变量准备在将来保存对象，建议用 null 初始化，这样只要直接检查 null 值就可以知道相应的变量是否被赋值过。
**undefined 的值是派生自 null 的，因此“==”会返回 true。**

#### 4.Boolean

true 不一定等于1，false 不一定等于0。
所有值都有与这两个 Boolean 值等价的值，要将一个值转换为对应的 Boolean值，可以使用 Boolean()。

|    数据类型    |      true      |      false      |
| ------------- |  -------------  | -------------- |
|    String    |  任何非空字符串  |  “”（空字符串） |
|    Number    |  任何非零数字值  |  0和 NaN |
|    Object    |  任何对象  |  null |
|    Undefined   |  n/a 不适用  |  undefined |

#### 5.Number

```
var octalNum = 070; // 八进制，第一位必须是0
var hexNum = 0xA； // 十六进制，前两位必须是0x
```
八进制和十六进制在计算时，都会转换成十进制数值。

##### 浮点数
所谓浮点数，就是必须包换一个小数点，并且小数点后面必须至少有一个数字，虽然小数点前面可以没有整数，但不推荐这种写法。
```
var floatNum = 3.125e7; // 31250000
```
浮点数最高精度是17位小数，但在进行算术计算的时候精度远远不如整数。例如0.1加0.2的结果不是0.3，而是0.3000000000000000004，舍入误差会导致无法测试浮点数值。

##### 数值范围
Number.MIN_VALUE 和 Number.MAX_VALUE，如果超出会自动换成特殊的 Infinity 的值，如果负数就是 -Infinity (负无穷)。可以用 isFinite() 函数判断。

##### NaN
即非数值，用来表示本来要返回数值的操作数未返回数值的情况（这样就不会跑出错误）。
NaN 与任何数值都不相等，可用 isNaN() 来判断，任何不能被转换成数值的值都会导致这个函数返回 true。

##### 数值转换
Number()：适用于任何数据类型。如果字符串是空的，则被转换成0；如果字符串不包含数字之类的，就会被转换成 NaN。
parseInt(), parseFloat()：专门把字符串转换成数值。

#### 6.浮点数
toString() 方法，转换为字符，可以输出二进制、八进制、十六进制。在不知道值是不是 null 或者 undefined 的情况下，还可以使用 String() 。

#### 7.Object
Object 每个实例都具有下列属性和方法：
* constructor：保存着用于创建当前对象的函数
* hasOwnProperty(propertyName)：检查给定的属性在当前对象实例中是否存在。
* isPrototypeOf(Object)：用于检查传入的对象是否是当前对象的原型。
* propertyIsEnumberable(propertyName)：用于检查给定属性能否使用 for-in 来枚举。
* toLocaleString(), toString(), valueOf()

### 操作符

#### 1.一元操作符
```
++ age;
age = age + 1; // 效果相同
```
```
var num1 = 2;
var num2 = 20;
var num3 = --num1 + num2; // 21
var num4 = num1 + num2; // 21
```
```
var num1 = 2;
var num2 = 20;
var num3 = num1-- + num2; // 22
var num4 = num1 + num2; // 21
```
一元加操作符，放在数值前面，不会对数值产生任何影响，在对非数值应用时，会像 Number() 一样对这个值进行转换。
一元减操作符，放在数值前面，数值变成负数，在对非数值应用时，和加操作符一样，最后再转为负数。

#### 2.位操作符
ECMAScript 中所有数值都按照 IEEE-754 64位的形式来存储，但未操作符不直接操作64位值，而是先转换成32位，执行操作，然后再转换成64位。
* ~：按位非，返回反码
* &：按位与
* |：按位或
* ^：按位异或
* <<：左移，以0填充
* >>：有符号右移，用符号位填充
* >>>：无符号右移，由于负数以二进制补码表示，所以结果相差很大
