---
layout: post
title: "利用jekyll搭建博客"
date: "2015-11-01"
slug: "利用jekyll搭建博客"
description: "将纯文本转换为静态博客网站，不再需要数据库，不需要开发评论功能，不需要不断的更新版本——只用关心你的博客内容。使用Markdown（或 Textile）、Liquid 和 HTML & CSS 构建可发布的静态网站将纯文本转换为静态博客网站，不再需要数据库，不需要开发评论功能，不需要不断的更新版本——只用关心你的博客内容。使用Markdown（或 Textile）、Liquid 和 HTML & CSS 构建可发布的静态网站."
category:
  - views
  - featured
# tags will also be used as html meta keywords.
tags:
  - 博客
  - jekyll
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
<!--more-->
### Inline HTML elements

HTML defines a long list of available inline tags, a complete list of which can be found on the [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

- **To bold text**, use `<strong>`.
- *To italicize text*, use `<em>`.
- Abbreviations, like <abbr title="HyperText Markup Langage">HTML</abbr> should use `<abbr>`, with an optional `title` attribute for the full phrase.
- Citations, like <cite>&mdash; Mark otto</cite>, should use `<cite>`.
- <del>Deleted</del> text should use `<del>` and <ins>inserted</ins> text should use `<ins>`.
- Superscript <sup>text</sup> uses `<sup>` and subscript <sub>text</sub> uses `<sub>`.

Most of these elements are styled by browsers with few modifications on our part.

## 安装Ruby环境

    安装地址: http://rubyinstaller.org/downloads/,   mac直接去官网下载
## 安装jekyll
使用 `gem install jekyll` 命令安装jekyll
