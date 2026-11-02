---
layout: page
title: 日常随笔
permalink: /essays/
---

记录生活里的细碎时刻、感受与思考。

## 全部文章

{% assign articles = site.posts | where_exp: "post", "post.categories contains 'essays'" %}
{% for post in articles %}
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})
{% else %}
这个栏目还没有文章。
{% endfor %}
