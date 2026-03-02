---
layout: page
title: Projects
permalink: /project/
---

{% assign projects = site.projects | sort: "date" | reverse %}

{% if projects and projects.size > 0 %}
<ul>
  {% for p in projects %}
    <li>
      <a href="{{ p.url | relative_url }}">{{ p.title }}</a>
      {% if p.status %}<small> — {{ p.status }}</small>{% endif %}
      {% if p.description %}<div>{{ p.description }}</div>{% endif %}
    </li>
  {% endfor %}
</ul>
{% else %}
<p>No projects yet.</p>
{% endif %}
