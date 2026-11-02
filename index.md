---
layout: default
title: 首页
---

<style>
.zoe-hero {
  text-align: center;
  padding: 55px 12px 45px;
}
.zoe-hero h1 {
  font-size: 2.1rem;
  line-height: 1.5;
  font-weight: 600;
}
.zoe-hero p {
  color: #777;
  line-height: 1.9;
}
.zoe-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 18px;
  margin: 25px 0 45px;
}
.zoe-card {
  border: 1px solid #e8e8e8;
  border-radius: 12px;
  padding: 23px 18px;
  color: inherit !important;
  text-decoration: none !important;
  transition: 0.2s;
}
.zoe-card:hover {
  box-shadow: 0 5px 20px rgba(0,0,0,0.07);
  transform: translateY(-3px);
}
.zoe-card h2 {
  font-size: 1.3rem;
  margin: 15px 0 10px;
}
.zoe-card p {
  font-size: 0.9rem;
  color: #777;
  line-height: 1.8;
}
.zoe-icon { font-size: 2rem; }
.zoe-articles { margin: 35px 0; }
.zoe-articles h2 { font-size: 1.3rem; }
.zoe-articles ul {
  list-style: none;
  margin-left: 0;
}
.zoe-articles li {
  padding: 11px 0;
  border-bottom: 1px solid #eee;
}
.zoe-date {
  color: #999;
  font-size: 0.85rem;
  margin-right: 15px;
}
.zoe-more {
  display: inline-block;
  margin-top: 15px;
}
@media (max-width: 650px) {
  .zoe-grid { grid-template-columns: 1fr; }
  .zoe-hero h1 { font-size: 1.6rem; }
}
</style>

<div class="zoe-hero">
  <h1>记录生活，保持阅读，持续成长。</h1>
  <p>
    一个记录日常、分享阅读、探索自我的小小空间。<br>
    在这里，留下时间走过的痕迹。
  </p>
</div>

<div class="zoe-grid">

  <a href="{{ '/essays/' | relative_url }}" class="zoe-card">
    <div class="zoe-icon">☕</div>
    <h2>日常随笔</h2>
    <p>生活里的细碎时刻，值得被认真记录。</p>
    <span>探索更多 →</span>
  </a>

  <a href="{{ '/books/' | relative_url }}" class="zoe-card">
    <div class="zoe-icon">📖</div>
    <h2>读书笔记</h2>
    <p>在书页之间，与不同的思想相遇。</p>
    <span>探索更多 →</span>
  </a>

  <a href="{{ '/growth/' | relative_url }}" class="zoe-card">
    <div class="zoe-icon">🌱</div>
    <h2>学习成长</h2>
    <p>保持好奇，慢慢成为更好的自己。</p>
    <span>探索更多 →</span>
  </a>

</div>

<div class="zoe-articles">
  <h2>☕ 日常随笔</h2>
  {% assign essays = site.posts | where_exp: "post", "post.categories contains 'essays'" %}
  <ul>
  {% for post in essays limit:3 %}
    <li>
      <span class="zoe-date">{{ post.date | date: "%Y-%m-%d" }}</span>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </li>
  {% else %}
    <li>暂无文章，等待新的故事。</li>
  {% endfor %}
  </ul>
  <a class="zoe-more" href="{{ '/essays/' | relative_url }}">查看全部随笔 →</a>
</div>

<div class="zoe-articles">
  <h2>📖 读书笔记</h2>
  {% assign books = site.posts | where_exp: "post", "post.categories contains 'books'" %}
  <ul>
  {% for post in books limit:3 %}
    <li>
      <span class="zoe-date">{{ post.date | date: "%Y-%m-%d" }}</span>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </li>
  {% else %}
    <li>暂无文章，下一本好书正在路上。</li>
  {% endfor %}
  </ul>
  <a class="zoe-more" href="{{ '/books/' | relative_url }}">查看全部读书笔记 →</a>
</div>

<div class="zoe-articles">
  <h2>🌱 学习成长</h2>
  {% assign growth = site.posts | where_exp: "post", "post.categories contains 'growth'" %}
  <ul>
  {% for post in growth limit:3 %}
    <li>
      <span class="zoe-date">{{ post.date | date: "%Y-%m-%d" }}</span>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </li>
  {% else %}
    <li>暂无文章，成长从今天开始。</li>
  {% endfor %}
  </ul>
  <a class="zoe-more" href="{{ '/growth/' | relative_url }}">查看全部成长记录 →</a>
</div>
  
