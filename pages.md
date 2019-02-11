---
layout: page
title: Posts
permalink: /pages/
---
<ul>
  {% for post in site.categories.work %}
    {% if post.url %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
        {{ post.date }}
    {% endif %}
  {% endfor %}
</ul>