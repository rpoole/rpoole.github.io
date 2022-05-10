---
title: ''
---

I'll mainly post about trying to (for the first time in my life) finish a side
project.

<hr>

{% for post in site.posts %}
<div style="margin-top: 40px">
  <h2>
    <a href="{{ post.url }}">{{ post.title }}</a>
  </h2>
  <i class="gray-text" style="font-size: 90%">{{ post.date | date: "%B %d, %Y" }}</i>
  <div class="gray-text" style="margin-top: 10px; padding-left: 10px; border-left: 5px solid #ddd;">
    {{ post.content | markdownify | strip_html | truncatewords: 50 }}
  </div>
</div>
{% endfor %}
