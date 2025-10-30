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
  <li style="margin: 0 0 1rem 0;">
    <a href="{{ post.url | relative_url }}"><strong>{{ post.title }}</strong></a>
    <small>（{{ post.date | date: "%Y-%m-%d" }}）</small><br>
    {%- if post.description -%}
      {{ post.description }}
    {%- else -%}
      {{ post.excerpt | strip_html | truncate: 120 }}
    {%- endif -%}
    <a href="{{ post.url | relative_url }}">閱讀更多 →</a>
  </li>
{%- endfor -%}
</ul>
