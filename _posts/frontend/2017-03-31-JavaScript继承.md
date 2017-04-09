---
layout: post
title: JavaScript继承
categories: frontend
catalog: true
original: true
tags: JavaScript
---

JavaScript中没有类的概念，靠原型链的方式来实现继承。

### 继承

##### 原型链继承

```js
    var Base = function()
    {
        this.level = 1;
        this.name = "base";
        this.toString = function(){
            return "base";
        };
    };
    Base.CONSTANT = "constant";

    var Sub = function()
    {
    };
    Sub.prototype = new Base();
    Sub.prototype.name = "sub";
```
优点：从instanceof关键字来看，实例既是父类的实例，又是子类的实例，看起来似乎是最纯粹的继承。

缺点：子类区别于父类的属性和方法，必须在Sub.prototype = new Base();这样的语句之后分别执行，无法被包装到Sub这个构造器里面去。
例如：Sub.prototype.name = “sub”；无法实现多重继承。


##### 构造继承

```js
    var Base = function()
    {
        this.level = 1;
        this.name = "base";
        this.toString = function(){
            return "base";
        };
    };
    Base.CONSTANT = "constant";

    var Sub = function()
    {
        Base.call(this);
        this.name = "sub";
    };
```

优点：可以实现多重继承，可以把子类特有的属性设置放在构造器内部。

缺点：使用instanceof发现，对象不是父类的实例。


##### 实例继承

```js
    var Base = function()
    {
        this.level = 1;
        this.name = "base";
        this.toString = function(){
            return "base";
        };
    };
    Base.CONSTANT = "constant";

    var Sub = function()
    {
        var instance = new Base();
        instance.name = "sub";
        return instance;
    };
```

优点：是父类的对象，并且使用new构造对象和不使用new构造对象，都可以获得相同的效果。

缺点：生成的对象实质仅仅是父类的实例，并非子类的对象；不支持多继承。

##### 拷贝继承

```js
    var Base = function()
    {
        this.level = 1;
        this.name = "base";
        this.toString = function(){
            return "base";
        };
    };
    Base.CONSTANT = "constant";

    var Sub = function()
    {
        var base = new Base();
        for(var i in base)
            Sub.prototype[i] = base[i];
        Sub.prototype["name"] = "sub";
    };
```
优点：支持多继承。

缺点：效率较低；无法获取父类不可枚举的方法。