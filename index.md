---
layout: default
title: Motorsport Software Notes
---

{% assign featured = site.posts | first %}
{% assign rest = site.posts | offset: 1 %}

<section class="home-hero">
  <a class="home-hero__bg" href="{{ featured.url | relative_url }}" aria-label="{{ featured.title }}">
    <img src="{{ featured.hero | relative_url }}" alt="{{ featured.hero_alt | default: featured.title }}">
  </a>

  <div class="home-hero__overlay"></div>

  <div class="home-hero__content">
    <div class="home-hero__kicker">Ultimo articolo</div>
    <h1 class="home-hero__title">{{ featured.title }}</h1>

    {% if featured.subtitle %}
      <p class="home-hero__text">{{ featured.subtitle }}</p>
    {% endif %}

    <div class="home-hero__buttons">
      <a class="button button--solid" href="{{ featured.url | relative_url }}">READ</a>
    </div>
  </div>
</section>

<section class="home-grid">
  <div class="home-grid__head">
    <h2 class="home-grid__title">Altri articoli</h2>
  </div>

  <div class="home-cards">
    {% for post in rest limit: 9 %}
      <article class="home-card">
        <a class="home-card__media" href="{{ post.url | relative_url }}">
          {% if post.hero %}
            <img src="{{ post.hero | relative_url }}" alt="{{ post.hero_alt | default: post.title }}">
          {% else %}
            <div class="home-card__placeholder"></div>
          {% endif %}
        </a>

        <div class="home-card__body">
          <h3 class="home-card__title">
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
          </h3>

          {% if post.subtitle %}
            <p class="home-card__text">{{ post.subtitle }}</p>
          {% endif %}

          <div class="home-card__meta">
            {% if post.date %}
              <span class="home-card__date">{{ post.date | date: "%d/%m/%Y" }}</span>
            {% endif %}
            <a class="home-card__read" href="{{ post.url | relative_url }}">READ</a>
          </div>
        </div>
      </article>
    {% endfor %}
  </div>
</section>