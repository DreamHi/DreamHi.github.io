---
layout: post
title: JavaScript函数
categories: frontend
catalog: true
original: true
---

函数的概念在JavaScript中非常重要,是第一型对象(first-class object)。函数可以被声明，引用，也可以当作参数传递，还能被调用。

函数是第一型对象的功能：
* 它们可以通过字面量进行创建
* 它们可以赋值给变量，数组或其他对象的属性
* 它们可以作为参数传递给函数
* 它们可以作为函数的返回值进行返回
* 它们可以拥有动态创建并赋值的属性

### 函数是第一型对象的例子
-------------------------
#### 它们可以通过字面量进行创建

字面量函数由4部分组成：function，函数名, (可选参数), {函数体}
函数也可以没有名字，称为匿名函数。回调函数或者函数当变量时一般是匿名的。

```js
// ES5
 function output() {
     console.log("Hello World.");
 }
```

#### 它们可以赋值给变量，数组或其他对象的属性

```js
// ES6
// 变量
const funVal = () => console.log("Hello World");

// 数组
const funArr = [];
funArr[0] = funVal;

// 对象的属性
const funObj = {
    name: "output",
    func: () => {
        console.log("Hello World");
    }
}
```

#### 它们可以作为参数传递给函数

#### 它们可以作为函数的返回值进行返回

#### 它们可以拥有动态创建并赋值的属性
