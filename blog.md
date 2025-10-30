---
layout: default
title: 部落格 Blog
lang: zh
permalink: /blog/
---

# 部落格 Blog

<ul class="post-list">
  {%- assign posts_zh = site.posts | where: "lang", "zh" | sort: "date" | reverse -%}
  {%- for post in posts_zh -%}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <small>（{{ post.date | date: "%Y-%m-%d" }}）</small>
    </li>
  {%- endfor -%}
</ul>
