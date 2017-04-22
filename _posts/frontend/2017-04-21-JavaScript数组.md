---
layout: post
title: JavaScript数组
categories: frontend
catalog: true
original: true
tags:
---

JS中数组的特点
* 数组的中可以存储多种类型的数据，一般不会这么用。
* 数组大小自动调整

## 数组定义
```js
// 定义
const names = ["王一","李二","张三"];
names[0];  // 王一
names.length; // 3
names[3];  // undefined

// 数组的长度可以改变,长度减少时，末尾的数据项会移除。增加时，每新增的项值都是undefined.
names.length = 1;
names[1]; // undefined
names.length = 10;
names[9]; // undefined

// 数组的最大项：4294967295
```

## 操作
### 栈 (LIFO:后进先出)
* push()
* pop()

```js
const names = ["王一","李二"];
names.push("张三"); // "王一","李二","张三"
names.pop(); // "王一","李二"
```

### 队(FIFO:先进先出)
* push()
* shift()

```js
const names = ["王一","李二"];
names.push("张三"); // "王一","李二","张三"
names.shift();  // "李二","张三"
```
### 逆队
* unshift()
* pop()

```js
const names = ["王一","李二"];
names.unshift("张三");  // "张三","王一","李二"
names.pop(); // "张三", "王一"
```
### 添加/缩小

* concat() 数组拼接

```js
const a = ["a", "b", "c"];
const b = ["x", "y", "z"];
const c = a.concat(b);
// a = ["a", "b", "c"]
// b = ["x", "y", "z"]
// c = ["a", "b", "c","x", "y", "z"]
```

* slice() 子数组

```js
const a = ["a", "b", "c"];
const b = a.slice(0,1) // ["a"]
const c = a.slice(1) // ["b", "c"]
const d = a.slice(1,2) // ["b"]
const e = a.slice(); // ["a", "b", "c"] copy
```

* splice() 向/从数组中添加/删除项目，然后返回被删除的项目。该方法会改变原始数组。

```js
const a = ["a", "b", "c"];
const r = a.splice(1, 1, "ache", "bug");
// a = ["a","ache", "bug", "c"] 原始数组
// r = ["b"] 删除的元素

const a = ["a", "b", "c"];
const r = a.splice(1, 0, "ache", "bug");
// a = ["a", "ache", "bug", "b", "c"] 原始数组
// r = [] 删除的元素
```

* reduce()
* reduceRight()

### 迭代

* every()  对数组中的每一项运行给定函数，如果该函数对每一项都返回true，则返回true
* filter()  对数组中的每一项运行给定函数，返回该函数会返回true的项组成的数组
* forEach() 对数组中的每一项运行给定函数，遍历数组

```js
const fruits = ['Apple', 'Banana'];
fruits.forEach(function(item, index, array) {
  console.log(item, index, array);
});
// Apple 0 ["Apple", "Banana"]
// VM385:3 Banana 1 ["Apple", "Banana"]

```
* map() 对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。
* some() 对数组中的每一项运行给定函数，如果该函数对任一项返回true，则返回true

### 排序和输出

* reverse() 逆序 会修改原数组

```js
const a = [1, 24, 5, 7, 9, 10];
const b = a.reverse();
// a = [10, 9, 7, 5, 24, 1]
// b = [10, 9, 7, 5, 24, 1]
```

* sort() 当没有参数的时候会按字母表升序排序 会修改原数组

```js
const a = [1, 24, 5, 7, 9, 10];
const b = a.sort();
// a = [1, 10, 24, 5, 7, 9]
// b = [1, 10, 24, 5, 7, 9]
```

* join()

```js
const a = ["a", "b", "c"];
const b = a.join("-");
// b = "a-b-c"
```