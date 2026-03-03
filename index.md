---
layout: default
title: Motorsport Software Notes
---

<div id="chi-siamo" class="u-hero" style="background-image: url('{{ '/assets/img/tel.png' | relative_url }}')">
  <div class="u-hero__overlay"></div>

  <div class="u-hero__content">
    <h4>About</h4>
    <h1 class="u-hero__title">Motorsport Software Notes</h1>
    <p class="u-hero__lead">Practical notes on telemetry, strategy, and tooling. Built to be searchable and engineering-first.</p>

    <div class="u-hero__buttons">
      <a class="u-btn u-btn--primary" href="{{ '/articles/' | relative_url }}">Read articles</a>
      <a class="u-btn" href="{{ '/project/' | relative_url }}">Explore projects</a>
      <a class="u-btn" href="{{ '/idea/' | relative_url }}">Vision</a>
    </div>
  </div>

  <nav class="u-hero__social" aria-label="Useful links">
    <a class="u-icon-btn" href="{{ '/feed.xml' | relative_url }}" aria-label="RSS">RSS</a>
    {% if site.github and site.github.repository_url %}
      <a class="u-icon-btn" href="{{ site.github.repository_url }}" rel="noreferrer noopener" target="_blank" aria-label="GitHub">GitHub</a>
    {% endif %}
  </nav>
</div>

<div class="u-wrapper">
  <h1 class="u-section-title">Latest</h1>
  <div class="u-feature" aria-label="Featured project">
    {% assign featured = site.projects | where: 'title', 'Endurance Stint Decision System' | first %}
    {% if featured %}
      <div class="u-feature__card">
        <div class="u-feature__media">
          {% if featured.hero %}
            <img src="{{ featured.hero | relative_url }}" alt="{{ featured.title }}" loading="lazy">
          {% else %}
            <img src="{{ '/assets/cover/excel.svg' | relative_url }}" alt="{{ featured.title }}" loading="lazy">
          {% endif %}
        </div>
        <div class="u-feature__body">
          <span class="u-pill">Featured</span>
          <h2 class="u-feature__title">{{ featured.title }}</h2>
          <p class="u-feature__sub">{{ featured.subtitle }}</p>
          <div class="u-feature__actions">
            <a class="u-btn u-btn--primary" href="{{ featured.url | relative_url }}">Open project</a>
            <a class="u-btn" href="{{ '/project/' | relative_url }}">All projects</a>
          </div>
        </div>
      </div>
    {% endif %}
  </div>

  <section class="stats">
    <div class="stat">
      <div class="stat__value">{{ site.posts | size }}</div>
      <div class="stat__label">Articles</div>
    </div>

    <div class="stat">
      <div class="stat__value">
        {% assign projects_count = site.projects | size %}
        {{ projects_count }}
      </div>
      <div class="stat__label">Projects</div>
    </div>

    <div class="stat">
      <div class="stat__value">
        {% assign tags_count = site.tags | size %}
        {{ tags_count }}
      </div>
      <div class="stat__label">Topics</div>
    </div>
  </section>

  <div class="u-news-grid">
    {%- comment -%}Defensive de-duplication by URL (some deploy setups can surface duplicates){%- endcomment -%}
    {% assign _grouped_posts = site.posts | group_by: 'url' %}
    {% for g in _grouped_posts limit: 6 %}
      {% assign post = g.items[0] %}
      <div class="u-news-card">
        <div class="u-news-card__img">
          {% if post.hero %}
            <img src="{{ post.hero | relative_url }}" alt="{{ post.hero_alt | default: post.title }}" loading="lazy">
          {% else %}
            <img src="{{ '/assets/cover/notes.jpg' | relative_url }}" alt="{{ post.title }}" loading="lazy">
          {% endif %}
        </div>
        <div class="u-news-card__body">
          <h2>{{ post.title }}</h2>
          <p>{{ post.subtitle | default: post.excerpt | strip_html | truncate: 120 }}</p>
          <div class="u-news-card__actions">
            <a class="u-btn" href="{{ post.url | relative_url }}">Read</a>
          </div>
        </div>
      </div>
    {% endfor %}
  </div>

  <div class="u-home-ctas" aria-label="Browse all content">
    <a class="u-btn u-btn--primary" href="{{ '/project/' | relative_url }}">All projects</a>
    <a class="u-btn" href="{{ '/articles/' | relative_url }}">All articles</a>
    <a class="u-btn" href="{{ '/search/' | relative_url }}">Search</a>
  </div>
</div>
