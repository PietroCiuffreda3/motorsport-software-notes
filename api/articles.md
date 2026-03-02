---
layout: page
title: Articles
permalink: /articles/
---

{% assign posts = site.posts %}

<ul>
  {% for post in posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      {% if post.date %}<small> — {{ post.date | date: "%d/%m/%Y" }}</small>{% endif %}
      {% if post.subtitle %}<div>{{ post.subtitle }}</div>{% endif %}
    </li>
  {% endfor %}
</ul>
