---
layout: post
title: "getComputedStyle方法"
date: "2016-6-13"
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
{% highlight bash %}
// 语法：
// 在旧版本之前，第二个参数“伪类”是必需的，现代浏览器已经不是必需参数了
// 如果不是伪类，设置为null，
window.getComputedStyle("元素", "伪类");
{% endhighlight %}
返回的内容是当前元素最终使用的所有的CSS样式，是一个对象。如下：
![getComputedStyle](http://octkdemet.bkt.clouddn.com/getComputedstyle.png "getComputedStyle")

 getComputedStyle 方法是只读，而element.style 是可读可写的，另外，这两个方法还有一个区别：我们的样式表的表现有三种形式（内联、内部样式表，外联），element.style只能获取被这些样式表定义了的样式，而 getComputedStyle 能获取到所有的样式。

## getPropertyValue方法
这个方法可以获取CSS样式申明对象上的属性值（直接属性名称），例如：
{% highlight bash %}
window.getComputedStyle(element, null).getPropertyValue("float");
{% endhighlight %}

## 封装函数
{% highlight bash %}
getStyle: function(elem, style) {
		// 主流浏览器
		if (win.getComputedStyle) {
			return win.getComputedStyle(elem, null).getPropertyValue(style);
	}
}
{% endhighlight %}

## 应用场景
getComputedStyle方法用在伪类元素上，结合CSS3 media queries将大放异彩。CSS3 media queries是响应布局实现之利器，仅仅通过CSS做布局可能无法应对所有的交互要求。如何运用我们刚才说的伪类方法呢？在元素`:before`或`:after`伪类上设置content属性，同时隐藏，其背后的原理是，当屏幕宽度变化的时候，通过JS获取content内容，如"mobile" "desktop",从而控制页面的元素或者其他的一些交互内容
{% highlight bash %}
.cd-images-list:before{
		content:"mobile";
		display: none;

}
@media only screen and (min-width:768PX){
		.cd-images-list:before{
			content:"desktop"
	}
}
{% endhighlight %}
### 获取content的方法：
{% highlight bash %}
function MQ(ele) {
	return window.getComputedStyle(ele, '::before').getPropertyValue('content').replace(/'/g, "").replace(/"/g, "").split(', ');
}
{% endhighlight %}


关于伪元素的运用还有很多，路漫漫........
