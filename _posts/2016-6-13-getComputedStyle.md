---
layout: post
title: "getComputedStyle方法"
date: "2016-5-28"
slug: "getComputedStyle方法"
description: "getComputedStyle是一个可以获取当前元素所有最终使用的CSS属性值。返回的是一个CSS样式声明对象([object CSSStyleDeclaration]),jQuery底层运作就应用了getComputedStyle以及getPropertyValue方法。"
category:
  - views
  - featured
# tags will also be used as html meta keywords.
tags:
  - 博客
  - css
show_meta: true
comments: true
mathjax: true
gistembed: true
published: true
noindex: false
nofollow: false
# hide QR code, permalink block while printing.
hide_printmsg: false
# show post summary or full post in RSS feed.
summaryfeed: false
## for twitter summary card with squared image and page description or page excerpt:
# imagesummary: foo.png
## for twitter card with large image:
# imagefeature: "http://img.youtube.com/vi/VEIrQUXm_hY/0.jpg"
## for twitter video card: (active for this page)
---

getComputedStyle是一个可以获取当前元素所有最终使用的CSS属性值。返回的是一个CSS样式声明对象([object CSSStyleDeclaration])

<!--more-->

## 语法
`// 语法：
// 在旧版本之前，第二个参数“伪类”是必需的，现代浏览器已经不是必需参数了
// 如果不是伪类，设置为null，
window.getComputedStyle("元素", "伪类");
`
返回的内容是当前元素最终使用的所有的CSS样式，是一个对象。
![getComputedStyle](http://octkdemet.bkt.clouddn.com/getComputedstyle.png "getComputedStyle")



### 定义匿名函数
在闭包中定义自己的私有函数，做到不污染全局变量，这是常用的方式。!function(){}()也是匿名函数一种写法，因为javascript将function当作一个函数声明的开始，而函数声明后面不允许跟圆括号！然而函数表达式后面可以跟圆括号。要将函数声明转换成函数表达式，像上面给函数体加上圆括号即可。

###  内部结构
MODAL CLASS DEFINITION：类定义，定义了插件构造方法类及方法。

MODAL PLUGIN DEFINITION：插件定义，上面只是定义了插件的类，这里才是实现插件的地方。

MODAL NO CONFLICT:插件命名冲突解决

MODAL DATA-API：DATA-属性接口

### 构造函数
{% highlight bash %}
var Modal = function (element, options) {
  this.options        = options
  this.$body          = $(document.body)
  this.$element       = $(element)
  this.$backdrop      =
  this.isShown        = null
  this.scrollbarWidth = 0

  if (this.options.remote) {
	this.$element
	  .find('.modal-content')
	  .load(this.options.remote, $.proxy(function () {
		this.$element.trigger('loaded.bs.modal')
	  }, this))
  }
}
{% endhighlight %}
这个类封装了插件对象初始化所需的方法和属性。用户可以用自定义的options覆盖默认值	，相关代码在插件定义中

### 插件定义
{% highlight bash %}
function Plugin(option, relatedTarget) {
  return this.each(function () {
	var $this   = $(this)
	var data    = $this.data('bs.modal')
	var options = $.extend({}, Modal.DEFAULTS, $this.data(), typeof option == 'object' && option)

	if (!data) $this.data('bs.modal', (data = new Modal(this, options)))
	if (typeof option == 'string') data[option](relatedTarget)
	else if (options.show) data.show(relatedTarget)
  })
}

 $.fn.modal             = Plugin
 {% endhighlight %}


 通过在$.fn对象（插件的命名空间）下添加了modal属性，这样我们以后就可以通过$(selector).modal()来调用插件了。在jQuery中jQuery.fn正是jQuery.prototype，所以modal这个属性是实例属性

### 解决命名冲突
{% highlight bash %}
$.fn.modal.noConflict = function () {
  $.fn.modal = old
  return this
}
{% endhighlight %}

用法同$.noConflict，释放$.fn.modal的控制权，并重新为$.fn.modal声明一个名称，旨在解决插件名称和其他插件有冲突的情况

### Data属性接口

{% highlight bash %}
$(document).on('click.bs.modal.data-api', '[data-toggle="modal"]', function (e) {
  var $this   = $(this)
  var href    = $this.attr('href')
  var $target = $($this.attr('data-target')
  var option  = $target.data('bs.modal') ? 'toggle' : $.extend({ remote: !/#/.test(href) && href }, $target.data(), $this.data())

  if ($this.is('a')) e.preventDefault()

  $target.one('show.bs.modal', function (showEvent) {
	if (showEvent.isDefaultPrevented()) return // only register focus restorer if modal will actually get shown
	$target.one('hidden.bs.modal', function () {
	  $this.is(':visible') && $this.trigger('focus')
	})
  })
  Plugin.call($target, option, this)
})
{% endhighlight %}

向所有带有data-toggle以modal开头的元素绑定了click事件(注意这里用了事件委托的写法)

Bootstrap这种写插件的模式值得借鉴和学习，我已经在工作中使用了这种方式，用起来很方便。
