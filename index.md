---
title: ''
---

{% for post in site.posts %}
<style>
 .post:not(:last-child) {
    margin-bottom: 25px;
    border-bottom: 1px solid #ddd;
    padding-bottom: 25px;
  }
</style>
<div class="post">
  <a class="post-link" href="{{ post.url }}">
    <h3 class="post-header">
      {{ post.title }}
    </h3>
  </a>
  <i class="gray-text" style="font-size: 90%">{{ post.date | date: "%B %d, %Y" }}</i>
  <div style="margin-top: 10px;">
    {{ post.content | markdownify | strip_html | truncatewords: 50 }}
  </div>
</div>
{% endfor %}
