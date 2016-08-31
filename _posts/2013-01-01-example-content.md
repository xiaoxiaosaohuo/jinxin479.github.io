---
layout: post
title: "利用jekyll搭建静态博客"
date: "2015-08-01"
slug: "jekyll_content"
description: "利用jekyll搭建静态博客"
category:
  - views
  - featured
# tags will also be used as html meta keywords.
tags:
  - jekyll
  - common_tag
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
videocredit: tedtalks
---

    将纯文本转换为静态博客网站，不再需要数据库，不需要开发评论功能，不需要不断的更新版本——只用关心你的博客内容。使用Markdown（或 Textile）、Liquid 和 HTML & CSS 构建可发布的静态网站。
<!--more-->

* TOC
{:toc}

### 搭建jekyll博客
使用jekyll将markdown文件生成静态的html文件，并使用主题进行布局，形成最终的博客页面。
####安装Ruby环境
    安装地址: http://rubyinstaller.org/downloads/,   mac直接去官网下载
####安装jekyll
    使用 {% highlight bash %}
    gem install jekyll
    {% endhighlight %}命令安装jekyll
