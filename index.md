---
layout: default
title: 首页
---

<div class="zoe-archive">
  <header class="archive-intro">
    <p class="archive-eyebrow">文字 · 阅读 · 生活</p>
    <h1>记录生活，慢慢成长。</h1>
    <p>在这里，留下日常的片段、阅读的思考和成长的足迹。</p>
  </header>

  <nav class="archive-filters" aria-label="文章分类">
    <button type="button" data-category="all" aria-pressed="true">全部文章</button>
    <button type="button" data-category="essays" aria-pressed="false">日常随笔</button>
    <button type="button" data-category="books" aria-pressed="false">读书笔记</button>
    <button type="button" data-category="growth" aria-pressed="false">学习成长</button>
  </nav>
  <label class="archive-search">
    <span>搜索文章</span>
    <input id="article-search" type="search" placeholder="输入文章标题…" autocomplete="off">
  </label>
  <p class="archive-count" aria-live="polite">共 {{ site.posts.size }} 篇文章<span id="visible-count"></span></p>

  {% assign posts_by_year = site.posts | group_by_exp: "post", "post.date | date: '%Y'" %}
  {% for year in posts_by_year %}
  <details class="archive-year" open>
    <summary>{{ year.name }} <span class="year-count">{{ year.items.size }} 篇</span></summary>
    <ul class="archive-list">
      {% for post in year.items %}
      <li class="archive-row" data-categories="{{ post.categories | jsonify | escape }}">
        <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%m.%d" }}</time>
        <a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
        <span class="archive-category">{% if post.categories contains 'essays' %}日常随笔{% elsif post.categories contains 'books' %}读书笔记{% elsif post.categories contains 'growth' %}学习成长{% else %}其他{% endif %}</span>
      </li>
      {% endfor %}
    </ul>
  </details>
  {% endfor %}
  <p id="archive-empty" {% if site.posts.size > 0 %}hidden{% endif %}>这里还没有匹配的文章，换个分类或关键词试试。</p>
</div>

<script>
(() => {
  const root = document.querySelector('.zoe-archive');
  const buttons = [...root.querySelectorAll('[data-category]')];
  const rows = [...root.querySelectorAll('.archive-row')];
  const years = [...root.querySelectorAll('.archive-year')];
  const input = root.querySelector('#article-search');
  let category = 'all';
  function update() {
    const query = input.value.trim().toLocaleLowerCase();
    let count = 0;
    rows.forEach(row => {
      const categories = JSON.parse(row.dataset.categories);
      const match = (category === 'all' || categories.includes(category)) &&
        row.querySelector('a').textContent.toLocaleLowerCase().includes(query);
      row.hidden = !match;
      if (match) count++;
    });
    years.forEach(year => {
      const visible = [...year.querySelectorAll('.archive-row')].filter(row => !row.hidden).length;
      year.hidden = visible === 0;
      year.querySelector('.year-count').textContent = visible + ' 篇';
      if (query || category !== 'all') year.open = true;
    });
    root.querySelector('#visible-count').textContent = ' · 当前显示 ' + count + ' 篇';
    root.querySelector('#archive-empty').hidden = count !== 0;
    buttons.forEach(button => button.setAttribute('aria-pressed', String(button.dataset.category === category)));
  }
  buttons.forEach(button => button.addEventListener('click', () => {
    category = button.dataset.category;
    update();
  }));
  input.addEventListener('input', update);
  update();
})();
</script>
