---
layout: default
title: AI Wiki Index
---

# 🧠 AI Wiki – Recent Articles

Here are the latest articles:

<ul>
  {% assign sorted_posts = site.pages | where_exp: "page", "page.path contains 'posts/' and page.title" | sort: "date" | reverse %}
  {% for page in sorted_posts %}
    {% if page.url contains 'posts/' %}
      <li>
        <a href="{{ page.url | relative_url }}">{{ page.title }}</a>
        <small>({{ page.date | date: "%Y-%m-%d" }})</small>
      </li>
    {% endif %}
  {% endfor %}
</ul>
