---
layout: post
title: jQueryPlugin开发
categories: frontend
catalog: true
original: true
tags: JavaScript jQuery 插件
---

开发插件的目的是为了功能或者代码复用。一个或多个功能封装成插件。
jQuery插件类似jQuery对象的一个方法。所有的juqery对象都可以使用

## 常见插件用法(自命名)

* 直接型（示例对象插件）

```js
$("DomId").pluginName();

```

* 内敛型（全局函数插件）

```js
$.pluginName("Object");

```

* 闷骚型

```js
只要在页面加载插件，就默认调用

```

* 总结：想知道优缺点是不，自己分析吧？95%的插件都是直接型，另外两种可以先不学。

### 官方分类

* 通过$.extend()来扩展jQuery
* 通过$.fn 向jQuery添加新的方法
* 通过$.widget()应用jQuery UI的部件工厂方式创建

#### 例子

```js
(function ( $ ) {
    $.fn.greenify = function( options ) {
        // This is the easiest way to have default options.
        var settings = $.extend({
            // These are the defaults.
            color: "#556b2f",
            backgroundColor: "white"
        }, options );

        // Greenify the collection based on the settings variable.
        this.css({
            color: settings.color,
            backgroundColor: settings.backgroundColor
        });

        return this；
    };
}( jQuery ));
```

#### 几个概念

  $: jQuery别名
  fn：jQuery的prototype对象的别名. $.fn(jQuery.prototype)
  this: 插件内部this = $, 插件函数内this = dom元素。
  chaining: "return this"为了jQuery对象的链接操作。$( "a" ).greenify().addClass( "greenified" );
  保护别名：为了能在插件内部使用$,插件结构 (function($){...}(jQuery))
  $.extend: 扩展对象的方法. $.extend(boolean,dest,src1,src2,src3...)

### 开发插件需要准备什么

* 插件名
* 插件功能整理
* 默认属性
* 自定义属性
* 插件的扩展接口

### 开发模板（面向对象的插件开发）

```js
/* ========================================================================
 * Bootstrap: alert.js v3.3.5
 * http://getbootstrap.com/javascript/#alerts
 * ========================================================================
 * Copyright 2011-2015 Twitter, Inc.
 * Licensed under MIT (https://github.com/twbs/bootstrap/blob/master/LICENSE)
 * ======================================================================== */

+function ($) {
  'use strict';

  // ALERT CLASS DEFINITION
  // ======================

  var dismiss = '[data-dismiss="alert"]'
  var Alert   = function (el) {
    $(el).on('click', dismiss, this.close)
  }

  Alert.VERSION = '3.3.5'

  Alert.TRANSITION_DURATION = 150

  Alert.prototype.close = function (e) {
    var $this    = $(this)
    var selector = $this.attr('data-target')

    if (!selector) {
      selector = $this.attr('href')
      selector = selector && selector.replace(/.*(?=#[^\s]*$)/, '') // strip for ie7
    }

    var $parent = $(selector)

    if (e) e.preventDefault()

    if (!$parent.length) {
      $parent = $this.closest('.alert')
    }

    $parent.trigger(e = $.Event('close.bs.alert'))

    if (e.isDefaultPrevented()) return

    $parent.removeClass('in')

    function removeElement() {
      // detach from parent, fire event then clean up data
      $parent.detach().trigger('closed.bs.alert').remove()
    }

    $.support.transition && $parent.hasClass('fade') ?
      $parent
        .one('bsTransitionEnd', removeElement)
        .emulateTransitionEnd(Alert.TRANSITION_DURATION) :
      removeElement()
  }


  // ALERT PLUGIN DEFINITION
  // =======================

  function Plugin(option) {
    return this.each(function () {
      var $this = $(this)
      var data  = $this.data('bs.alert')

      if (!data) $this.data('bs.alert', (data = new Alert(this)))
      if (typeof option == 'string') data[option].call($this)
    })
  }

  var old = $.fn.alert

  $.fn.alert             = Plugin
  $.fn.alert.Constructor = Alert


  // ALERT NO CONFLICT
  // =================

  $.fn.alert.noConflict = function () {
    $.fn.alert = old
    return this
  }


  // ALERT DATA-API
  // ==============

  $(document).on('click.bs.alert.data-api', dismiss, Alert.prototype.close)

}(jQuery);

```