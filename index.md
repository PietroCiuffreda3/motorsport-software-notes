---
layout: default
title: Motorsport Software Notes
---

{% assign featured_posts = site.posts | slice: 0, 4 %}

<section class="x-hero">
  <div class="x-wrap">
    <div class="x-hero__top">
      <h1 class="x-hero__title">Motorsport Software Notes</h1>
      <p class="x-hero__sub">Telemetry, strategy, tooling, and engineering notes — built like a fast newsroom, curated like a lab notebook.</p>
    </div>
  </div>

  <div class="x-carousel" aria-label="Featured">
    <div class="x-carousel__track">
      {% for post in featured_posts %}
        <a class="x-slide" href="{{ post.url | relative_url }}" aria-label="{{ post.title }}">
          <div class="x-slide__media" style="background-image: url('{{ post.hero | relative_url }}');"></div>
          <div class="x-slide__fade"></div>
          <div class="x-slide__body">
            <div class="x-pill">Featured</div>
            <div class="x-slide__title">{{ post.title }}</div>
            {% if post.subtitle %}
              <div class="x-slide__sub">{{ post.subtitle }}</div>
            {% endif %}
          </div>
        </a>
      {% endfor %}
    </div>
  </div>
</section>

<section class="x-section">
  <div class="x-wrap">
    <div class="x-section__head">
      <h2 class="x-h2">Latest articles</h2>
      <a class="x-cta" href="{{ '/articles/' | relative_url }}">View all</a>
    </div>

    <div class="x-grid">
      {% for post in site.posts limit: 9 %}
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

{% if site.projects and site.projects.size > 0 %}
<section class="x-section">
  <div class="x-wrap">
    <div class="x-section__head">
      <h2 class="x-h2">Projects</h2>
      <a class="x-cta" href="{{ '/project/' | relative_url }}">View all</a>
    </div>

    <div class="x-grid x-grid--3">
      {% for p in site.projects limit: 6 %}
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
            </div>
            <h3 class="x-card__title"><a href="{{ p.url | relative_url }}">{{ p.title }}</a></h3>
            {% if p.subtitle %}<p class="x-card__sub">{{ p.subtitle }}</p>{% endif %}
          </div>
        </article>
      {% endfor %}
    </div>
  </div>
</section>
{% endif %}