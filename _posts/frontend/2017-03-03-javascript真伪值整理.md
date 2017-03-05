---
layout: post
comments: JavaScript 真伪值整理
categories: javascript
catalog: true
tags: JavaScript
---
## 真伪值

### JavaScript 真伪值

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
