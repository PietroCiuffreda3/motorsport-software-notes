---
layout: default
title: Search
permalink: /search/
---

<section class="x-page">
  <div class="x-wrap">
    <h1 class="x-h1">Search</h1>
    <p class="x-muted">Type to filter articles and projects.</p>

    <div class="x-searchpage">
      <input id="q" class="x-searchpage__input" type="search" placeholder="Search..." autocomplete="off" />
      <div class="x-searchpage__meta" id="meta"></div>
    </div>

    <div class="x-results" id="results"></div>
  </div>
</section>

<script>
(function(){
  const params = new URLSearchParams(window.location.search);
  const initial = params.get('q') || '';

  const input = document.getElementById('q');
  const results = document.getElementById('results');
  const meta = document.getElementById('meta');
  if (!input || !results) return;

  const data = [
    {% for post in site.posts %}
      {
        type: 'Article',
        title: {{ post.title | jsonify }},
        subtitle: {{ post.subtitle | default: '' | jsonify }},
        url: {{ post.url | relative_url | jsonify }},
        date: {{ post.date | date: '%Y-%m-%d' | jsonify }},
        hero: {{ post.hero | default: '' | relative_url | jsonify }}
      }{% unless forloop.last %},{% endunless %}
    {% endfor %}
    {% if site.projects and site.projects.size > 0 %},{% endif %}
    {% for p in site.projects %}
      {
        type: 'Project',
        title: {{ p.title | jsonify }},
        subtitle: {{ p.subtitle | default: '' | jsonify }},
        url: {{ p.url | relative_url | jsonify }},
        date: {{ p.date | default: '' | jsonify }},
        hero: {{ p.hero | default: '' | relative_url | jsonify }}
      }{% unless forloop.last %},{% endunless %}
    {% endfor %}
  ];

  function normalize(s){ return (s || '').toString().toLowerCase().trim(); }

  function render(items){
    results.innerHTML = '';
    meta.textContent = items.length ? (items.length + ' results') : 'No results';

    items.slice(0, 50).forEach(item => {
      const card = document.createElement('a');
      card.className = 'x-result';
      card.href = item.url;

      const media = document.createElement('div');
      media.className = 'x-result__media';
      if (item.hero) {
        const img = document.createElement('img');
        img.loading = 'lazy';
        img.src = item.hero;
        img.alt = item.title;
        media.appendChild(img);
      } else {
        media.innerHTML = '<div class="x-result__ph"></div>';
      }

      const body = document.createElement('div');
      body.className = 'x-result__body';
      body.innerHTML = `
        <div class="x-result__top">
          <span class="x-pill">${item.type}</span>
          ${item.date ? `<span class="x-date">${item.date}</span>` : ''}
        </div>
        <div class="x-result__title">${item.title}</div>
        ${item.subtitle ? `<div class="x-result__sub">${item.subtitle}</div>` : ''}
      `;

      card.appendChild(media);
      card.appendChild(body);
      results.appendChild(card);
    });
  }

  function run(){
    const q = normalize(input.value);
    if (!q) return render(data);
    const out = data.filter(item => {
      const hay = normalize(item.title + ' ' + item.subtitle);
      return hay.includes(q);
    });
    render(out);
  }

  input.value = initial;
  input.addEventListener('input', run);
  run();
})();
</script>
