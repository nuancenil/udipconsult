---
layout: default
title: 部落格 Blog
lang: zh
en_url: /en/blog/
permalink: /blog/
---
<ul>
{%- assign posts_zh = site.posts | where: "lang", "zh" -%}
{%- for post in posts_zh -%}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <small>({{ post.date | date: "%Y-%m-%d" }})</small>
  </li>
{%- endfor -%}
</ul>
