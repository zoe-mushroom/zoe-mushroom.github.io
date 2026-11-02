---
layout: page
title: 读书笔记
permalink: /books/
---

读过的书、记下的句子，以及阅读带来的新思考。

## 全部文章

{% assign articles = site.posts | where_exp: "post", "post.categories contains 'books'" %}
{% for post in articles %}
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})
{% else %}
这个栏目还没有文章。
{% endfor %}
