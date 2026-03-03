---
layout: page
title: Articles
permalink: /articles/
---

<section class="x-page">
  <div class="x-wrap">
    <h1 class="x-h1">Articles</h1>
    <p class="x-muted">All notes, ordered by date.</p>

    <div class="x-grid">
      {%- comment -%}Defensive de-duplication by URL (some deploy setups can surface duplicates){%- endcomment -%}
      {% assign _grouped_posts = site.posts | group_by: 'url' %}
      {% for g in _grouped_posts %}
        {% assign post = g.items | first %}
        <article class="x-card">
          <a class="x-card__media" href="{{ post.url | relative_url }}">
            {% if post.hero %}
              <img src="{{ post.hero | relative_url }}" alt="{{ post.hero_alt | default: post.title }}" loading="lazy">
            {% else %}
              <div class="x-card__ph"></div>
            {% endif %}
          </a>
          <div class="x-card__body">
            <div class="x-card__meta">
              <span class="x-pill x-pill--soft">Article</span>
              {% if post.date %}<span class="x-date">{{ post.date | date: "%d %b %Y" }}</span>{% endif %}
            </div>
            <h3 class="x-card__title"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
            {% if post.subtitle %}<p class="x-card__sub">{{ post.subtitle }}</p>{% endif %}
          </div>
        </article>
      {% endfor %}
    </div>
  </div>
</section>
