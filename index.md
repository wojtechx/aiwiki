---
layout: default
title: AI Wiki Index
---

# 🧠 AI Wiki - Recent Articles

Here are the latest articles:

<ul>
  {% assign sorted_posts = site.pages | where_exp: "page", "page.path contains 'posts/'" | sort: "date" | reverse %}
  {% for page in sorted_posts %}
    {% if page.title and page.url contains 'posts/' %}
      <li>
        <a href="{{ page.url }}">{{ page.title }}</a>
        <small>({{ page.date | date: "%Y-%m-%d" }})</small>
      </li>
    {% endif %}
  {% endfor %}
</ul>
