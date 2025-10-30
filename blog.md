---
layout: default
title: 部落格
lang: zh
en_url: /en/blog/
permalink: /blog/
---

<ul class="post-list">
{%- assign posts_zh = site.posts | where: "lang", "zh" -%}
{%- for post in posts_zh -%}
  <li>
    <a href="{{ post.url | relative_url }}"><strong>{{ post.title }}</strong></a>
    <small class="meta">（{{ post.date | date: "%Y-%m-%d" }}）</small>
    {%- if post.description -%}
      <div class="excerpt">{{ post.description }}</div>
    {%- endif -%}
  </li>
{%- endfor -%}
</ul>
