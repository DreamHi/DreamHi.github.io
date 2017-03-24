---
layout: post
comments: JavaScript 真伪值整理
categories: 前端
catalog: true
original: true
tags: JavaScript
---

JavaScript的真伪值判断，没有规律。只能死记硬背。
而且第三方工具库的判断和语言本身也有区别。
作为笔记，比较语言本身和underscore库的区别。

## JavaScript 真伪值

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
_.isEmpty(hoge) // false
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

### lodash
