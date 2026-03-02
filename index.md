---
layout: default
title: Motorsport Software Notes
---

{% assign featured_projects = site.projects | default: empty | slice: 0, 3 %}
{% assign featured_posts = site.posts | slice: 0, 3 %}

<div id="chi-siamo" class="u-hero" style="background-image: url('{{ '/assets/img/tel.png' | relative_url }}')">
  <div class="u-hero__overlay"></div>

  <div class="u-hero__content">
    <h4>Chi siamo</h4>
    <h1 class="u-hero__title">Motorsport Software Notes</h1>
    <p class="u-hero__lead">Appunti pratici su telemetria, strategia e tooling. Una raccolta pensata per essere consultabile e “engineering-first”.</p>

    <div class="u-hero__buttons">
      <a class="u-btn u-btn--primary" href="{{ '/articles/' | relative_url }}">Leggi gli articoli</a>
      <a class="u-btn" href="{{ '/project/' | relative_url }}">Esplora i progetti</a>
      <a class="u-btn" href="{{ '/idea/' | relative_url }}">Visione</a>
    </div>
  </div>

  <nav class="u-hero__social" aria-label="Link utili">
    <a class="u-icon-btn" href="{{ '/feed.xml' | relative_url }}" aria-label="RSS">RSS</a>
    {% if site.github and site.github.repository_url %}
      <a class="u-icon-btn" href="{{ site.github.repository_url }}" rel="noreferrer noopener" target="_blank" aria-label="GitHub">GitHub</a>
    {% endif %}
  </nav>
</div>

<div class="u-wrapper">
  <h1 class="u-section-title" id="highlights">Highlights</h1>
  <p class="u-section-sub">Una selezione rapida per iniziare.</p>

  <div class="u-slideshow">
    <div class="u-slides">
      {% if featured_projects and featured_projects.size > 0 %}
        {% for p in featured_projects %}
          <div class="u-slide">
            <h3>{{ p.title }}</h3>
            {% if p.hero %}
              <img class="u-slide__img" src="{{ p.hero | relative_url }}" alt="{{ p.title }}" loading="lazy">
            {% else %}
              <div class="u-slide__ph"></div>
            {% endif %}
            {% if p.subtitle %}<p>{{ p.subtitle }}</p>{% endif %}
            <a class="u-btn u-btn--primary" href="{{ p.url | relative_url }}">Apri</a>
          </div>
        {% endfor %}
      {% else %}
        {% for post in featured_posts %}
          <div class="u-slide">
            <h3>{{ post.title }}</h3>
            {% if post.hero %}
              <img class="u-slide__img" src="{{ post.hero | relative_url }}" alt="{{ post.title }}" loading="lazy">
            {% else %}
              <div class="u-slide__ph"></div>
            {% endif %}
            {% if post.subtitle %}<p>{{ post.subtitle }}</p>{% endif %}
            <a class="u-btn u-btn--primary" href="{{ post.url | relative_url }}">Leggi</a>
          </div>
        {% endfor %}
      {% endif %}
    </div>

    <button class="u-nav u-nav--prev" type="button" aria-label="Precedente" onclick="uPlusSlides(-1)">‹</button>
    <button class="u-nav u-nav--next" type="button" aria-label="Successivo" onclick="uPlusSlides(1)">›</button>
  </div>

  <div class="u-dots" aria-label="Indicatori slideshow">
    <span class="u-dot" onclick="uCurrentSlide(1)" aria-label="Slide 1"></span>
    <span class="u-dot" onclick="uCurrentSlide(2)" aria-label="Slide 2"></span>
    <span class="u-dot" onclick="uCurrentSlide(3)" aria-label="Slide 3"></span>
  </div>
</div>

<div class="u-wrapper">
  <h1 class="u-section-title" id="contenuti">Contenuti</h1>
  <p class="u-section-sub">Sezioni principali del sito.</p>

  <div class="u-grid">
    <a class="u-card" href="{{ '/articles/' | relative_url }}">
      <h2>Articoli</h2>
      <p>Note, approfondimenti e walkthrough.</p>
      <span class="u-card__meta">{{ site.posts.size }} pubblicati</span>
    </a>
    <a class="u-card" href="{{ '/project/' | relative_url }}">
      <h2>Progetti</h2>
      <p>Tooling, template e risorse operative.</p>
      <span class="u-card__meta">{% if site.projects %}{{ site.projects.size }} voci{% else %}—{% endif %}</span>
    </a>
    <a class="u-card" href="{{ '/search/' | relative_url }}">
      <h2>Ricerca</h2>
      <p>Trova rapidamente un argomento.</p>
      <span class="u-card__meta">Query live</span>
    </a>
  </div>
</div>

<div class="u-wrapper">
  <h1 class="u-section-title">Ultime notizie</h1>
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
            <a class="u-btn" href="{{ post.url | relative_url }}">Leggi l'articolo</a>
          </div>
        </div>
      </div>
    {% endfor %}
  </div>
</div>

<script>
  let uSlideIndex = 1;
  function uShowSlides(n) {
    const slides = document.querySelectorAll('.u-slide');
    const dots = document.querySelectorAll('.u-dot');
    if (!slides.length) return;
    if (n > slides.length) uSlideIndex = 1;
    if (n < 1) uSlideIndex = slides.length;
    slides.forEach(s => s.style.display = 'none');
    dots.forEach(d => d.classList.remove('active'));
    slides[uSlideIndex - 1].style.display = 'block';
    if (dots[uSlideIndex - 1]) dots[uSlideIndex - 1].classList.add('active');
  }
  function uPlusSlides(n) { uShowSlides(uSlideIndex += n); }
  function uCurrentSlide(n) { uShowSlides(uSlideIndex = n); }
  document.addEventListener('DOMContentLoaded', () => uShowSlides(uSlideIndex));
</script>
