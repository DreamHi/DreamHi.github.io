---
layout: post
title: JavaScript真伪值整理
categories: frontend
catalog: true
original: true
tags: JavaScript
---

JavaScript中的真伪值和别的高级语言不一样，不是特别规范，有几个特殊的情况。
目前流行的第三方工具库中，对真伪值得判断也不统一，甚至和语言规范中定义的也不同。

## JavaScript中的真伪值

|值|类型|结果|
|--------|------|------|
|{}	|Object|	true|
|"hoge"	|String|	true|
|""	|String|	false|
|1	|Number|	true|
|-1	|Number|	true|
|0	|Number|	false|
|[]	|Array|	true|
|true	|Boolean|	true|
|false	|Boolean|	false|
|undefined|	undefined|	false|
|null	|null|	false|

### underscore1.8.3的判定方法

```js
_.isEmpty({})   // true
_.isEmpty("hoge") // false
_.isEmpty("") // true
_.isEmpty(1) // true
_.isEmpty(-1) // true
_.isEmpty(0) // true
_.isEmpty([]) // true
_.isEmpty(true) // true
_.isEmpty(false) // true
_.isEmpty(undefined) // true
_.isEmpty(null) // true
```

### lodash  4.17.4
```js
_.isEmpty({})   // true
_.isEmpty("hoge") // false
_.isEmpty("") // true
_.isEmpty(1) // true
_.isEmpty(-1) // true
_.isEmpty(0) // true
_.isEmpty([]) // true
_.isEmpty(true) // true
_.isEmpty(false) // true
_.isEmpty(undefined) // true
_.isEmpty(null) // true
```