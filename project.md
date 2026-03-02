---
layout: page
title: Projects
permalink: /project/
---

{% assign projects = site.projects | sort: "date" | reverse %}

<section class="x-page">
  <div class="x-wrap">
    <h1 class="x-h1">Projects</h1>
    <p class="x-muted">Tools, experiments, and prototypes.</p>

    {% if projects and projects.size > 0 %}
      <div class="x-grid x-grid--3">
        {% for p in projects %}
          <article class="x-card">
            <a class="x-card__media" href="{{ p.url | relative_url }}">
              {% if p.hero %}
                <img src="{{ p.hero | relative_url }}" alt="{{ p.title }}" loading="lazy">
              {% else %}
                <div class="x-card__ph"></div>
              {% endif %}
            </a>
            <div class="x-card__body">
              <div class="x-card__meta">
                <span class="x-pill x-pill--soft">Project</span>
                {% if p.status %}<span class="x-date">{{ p.status }}</span>{% endif %}
              </div>
              <h3 class="x-card__title"><a href="{{ p.url | relative_url }}">{{ p.title }}</a></h3>
              {% if p.subtitle %}
                <p class="x-card__sub">{{ p.subtitle }}</p>
              {% elsif p.description %}
                <p class="x-card__sub">{{ p.description }}</p>
              {% endif %}
            </div>
          </article>
        {% endfor %}
      </div>
    {% else %}
      <p class="x-muted">No projects yet.</p>
    {% endif %}
  </div>
</section>
