---
layout: default
title: Blog
lang: en
zh_url: /blog/
permalink: /en/blog/
---

<ul>
{%- assign posts_en = site.posts | where: "lang", "en" -%}
{%- for post in posts_en -%}
  <li><a href="{{ post.url }}">{{ post.title }}</a> <small>({{ post.date | date: "%Y-%m-%d" }})</small></li>
{%- endfor -%}
</ul>
