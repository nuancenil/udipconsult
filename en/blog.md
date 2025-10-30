---
layout: default
title: Blog
lang: en
zh_url: /blog/
permalink: /en/blog/
---

# Blog

<ul class="post-list">
  {%- assign posts_en = site.posts | where: "lang", "en" -%}
  {%- for post in posts_en -%}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <small>({{ post.date | date: "%b %-d, %Y" }})</small>
      {%- if post.description %}<div class="excerpt">{{ post.description }}</div>{% endif -%}
    </li>
  {%- endfor -%}
</ul>
