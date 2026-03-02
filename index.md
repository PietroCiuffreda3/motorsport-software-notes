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
  <h1 class="u-section-title" id="content">Content</h1>
  <p class="u-section-sub">Main areas of the site.</p>

  <div class="u-grid">
    <a class="u-card" href="{{ '/articles/' | relative_url }}">
      <h2>Articles</h2>
      <p>Notes, deep dives, and walkthroughs.</p>
      <span class="u-card__meta">{{ site.posts.size }} published</span>
    </a>
    <a class="u-card" href="{{ '/project/' | relative_url }}">
      <h2>Projects</h2>
      <p>Tooling, templates, and practical resources.</p>
      <span class="u-card__meta">{% if site.projects %}{{ site.projects.size }} items{% else %}—{% endif %}</span>
    </a>
    <a class="u-card" href="{{ '/search/' | relative_url }}">
      <h2>Search</h2>
      <p>Find a topic quickly.</p>
      <span class="u-card__meta">Live query</span>
    </a>
  </div>
</div>

<div class="u-wrapper">
  <h1 class="u-section-title">Latest</h1>
  <div class="u-news-grid">
    {% for post in site.posts limit: 6 %}
      <div class="u-news-card">
        <div class="u-news-card__img">
          {% if post.hero %}
            <img src="{{ post.hero | relative_url }}" alt="{{ post.hero_alt | default: post.title }}" loading="lazy">
          {% else %}
            <img src="{{ '/assets/cover/telemetry.svg' | relative_url }}" alt="{{ post.title }}" loading="lazy">
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
</div>
