---
layout: post
title: "利用Jekyll搭建博客"
date: "2015-11-01"
slug: "利用Jekyll搭建博客"
description: "将纯文本转换为静态博客网站，不再需要数据库，不需要开发评论功能，不需要不断的更新版本——只用关心你的博客内容。使用Markdown（或 Textile）、Liquid 和 HTML & CSS 构建可发布的静态网站将纯文本转换为静态博客网站，不再需要数据库，不需要开发评论功能，不需要不断的更新版本——只用关心你的博客内容。使用Markdown（或 Textile）、Liquid 和 HTML & CSS 构建可发布的静态网站."
category:
  - views
  - featured
# tags will also be used as html meta keywords.
tags:
  - 博客
  - Jekyll
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

将纯文本转换为静态博客网站，不再需要数据库，不需要开发评论功能，不需要不断的更新版本——只用关心你的博客内容。

<!--more-->

## 安装Ruby环境
&emsp;&emsp;安装完成Jekyll可能需要花几分钟的时间，但非常简单。请确保你在系统里已经有如下配置。

* Ruby（including development headers, Jekyll 2 需要 v1.9.3 及以上版本，Jekyll 3 需要 v2 及以上版本）
* RubyGems
*  Linux, Un ix, or Mac OS X
* NodeJS, 或其他 JavaScript 运行环境（Jekyll 2 或更早版本需要 CoffeeScript 支持）。
* Python 2.7（Jekyll 2 或更早版本）
安装地址: http://rubyinstaller.org/downloads/,   mac直接去官网下载

## 安装Jekyll

&emsp;&emsp;安装 Jekyll 的最好方式就是使用 RubyGems. 你只需要打开终端输入以下命令就可以安装了：
使用 `gem install jekyll` 命令安装jekyll

## 使用Jekyll
&emsp;&emsp;创建博客目录，随便命名，如：my-site
{% highlight bash %}
~ $ jekyll new my-site  
~ $ cd my-site
~/my-site $ bundle install
~/my-site $ bundle exec jekyll serve
{% endhighlight %}

一个基本的 Jekyll 网站的目录结构一般是像这样的：
`.
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _site
├── .jekyll-metadata
└── index.html`
打开浏览器在地址栏输入： http://localhost:4000，就可以看到效果了，是不是很爽啊！
- *注意*：这几部有可能出错，如果说是该端口已经被绑定了，此时需要你手动到配置文件中修改，换一个端口。在 `_confit.yml`文件中增加：port:2000
![端口错误]({{ site.urlimg }}/media/jekyll-01.png "端口错误")
如果是bundle 不是内部命令
![错误]({{ site.urlimg }}/media/jekyll-02.png "错误")
请敲入命令`gem install bundle`安装bundle可以解决
