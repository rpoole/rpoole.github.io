---
layout: default
list_title: Posts
title: ''
---

I'll mostly post about trying to (for the first time in my life) finish a side
project.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
