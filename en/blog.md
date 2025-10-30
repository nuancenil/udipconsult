---
layout: default
title: Blog
lang: en
permalink: /en/blog/
---

# Blog

<ul class="post-list">
  {%- assign posts_en = site.posts | where: "lang", "en" | sort: "date" | reverse -%}
  {%- for post in posts_en -%}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <small>({{ post.date | date: "%b %-d, %Y" }})</small>
    </li>
  {%- endfor -%}
</ul>
