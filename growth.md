---
layout: page
title: 学习成长
permalink: /growth/
---

记录新知识、新技能，以及一路上的探索和成长。

## 全部文章

{% assign articles = site.posts | where_exp: "post", "post.categories contains 'growth'" %}
{% for post in articles %}
- {{ post.date | date: "%Y-%m-%d" }} · [{{ post.title }}]({{ post.url | relative_url }})
{% else %}
这个栏目还没有文章。
{% endfor %}
