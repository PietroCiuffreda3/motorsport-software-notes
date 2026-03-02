---
layout: default
title: Motorsport Software Notes
---

{% assign featured = site.posts | first %}

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
      <a class="button button--solid" href="{{ featured.url | relative_url }}">Leggi</a>
      <a class="button" href="{{ '/articles/' | relative_url }}">Tutti gli articoli</a>
    </div>
  </div>
</section>