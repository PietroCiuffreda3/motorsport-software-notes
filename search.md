---
layout: default
title: Search
permalink: /search/
---

<section class="x-page">
  <div class="x-wrap">
    <h1 class="x-h1">Search</h1>
    <p class="x-muted">Type to filter articles, projects, and results.</p>

    <div class="x-searchpage">
      <input
        id="q"
        class="x-searchpage__input"
        type="search"
        placeholder="Search…"
        autocomplete="off"
        spellcheck="false"
        aria-label="Search"
      />
      <div class="x-searchpage__meta" id="meta" aria-live="polite"></div>
    </div>

    <div class="x-results" id="results"></div>
  </div>
</section>

<script>
(function(){
  const input   = document.getElementById('q');
  const results = document.getElementById('results');
  const meta    = document.getElementById('meta');
  if (!input || !results || !meta) return;

  // --- Build index (Liquid -> JS pushes) ---
  const data = [];

  // De-dupe posts at build-time (Jekyll can pick up duplicates if you have mirrored folders).
  {% assign unique_posts = site.posts | group_by: 'url' %}
  {% for g in unique_posts %}
    {% assign post = g.items[0] %}
    data.push({
      type: 'Article',
      title: {{ post.title | jsonify }},
      subtitle: {{ post.subtitle | default: '' | jsonify }},
      url: {{ post.url | relative_url | jsonify }},
      date: {{ post.date | date: '%Y-%m-%d' | jsonify }},
      hero: {{ post.hero | default: '' | relative_url | jsonify }}
    });
  {% endfor %}

  {% if site.projects and site.projects.size > 0 %}
    {% for p in site.projects %}
      data.push({
        type: 'Project',
        title: {{ p.title | jsonify }},
        subtitle: {{ p.subtitle | default: '' | jsonify }},
        url: {{ p.url | relative_url | jsonify }},
        date: {{ p.date | default: '' | jsonify }},
        hero: {{ p.hero | default: '' | relative_url | jsonify }}
      });
    {% endfor %}
  {% endif %}

  {% if site.results and site.results.size > 0 %}
    {% for r in site.results %}
      data.push({
        type: 'Result',
        title: {{ r.title | jsonify }},
        subtitle: {{ r.subtitle | default: '' | jsonify }},
        url: {{ r.url | relative_url | jsonify }},
        date: {{ r.date | default: '' | jsonify }},
        hero: {{ r.image | default: r.hero | default: '' | relative_url | jsonify }}
      });
    {% endfor %}
  {% endif %}

  // --- Runtime hardening: de-dupe by URL again ---
  const seen = new Set();
  const unique = [];
  for (const item of data) {
    if (!item || !item.url) continue;
    if (seen.has(item.url)) continue;
    seen.add(item.url);
    unique.push(item);
  }

  // --- Helpers ---
  function normalize(s){
    return (s || '')
      .toString()
      .toLowerCase()
      .normalize('NFD')
      .replace(/[\u0300-\u036f]/g, '')
      .trim();
  }

  function escapeHtml(s){
    return (s || '').toString()
      .replace(/&/g,'&amp;')
      .replace(/</g,'&lt;')
      .replace(/>/g,'&gt;')
      .replace(/"/g,'&quot;')
      .replace(/'/g,'&#039;');
  }

  function parseQuery(){
    const params = new URLSearchParams(window.location.search);
    return params.get('q') || '';
  }

  function setQueryParam(q){
    const params = new URLSearchParams(window.location.search);
    if (q) params.set('q', q);
    else params.delete('q');
    const next = `${window.location.pathname}${params.toString() ? '?' + params.toString() : ''}`;
    window.history.replaceState({}, '', next);
  }

  // Basic scoring so relevant items rise to the top.
  function scoreItem(item, q){
    const title = normalize(item.title);
    const sub   = normalize(item.subtitle);
    const hay   = `${title} ${sub}`.trim();

    if (!q) return 0;

    let score = 0;

    // Exact-ish
    if (title === q) score += 1000;

    // Prefix match
    if (title.startsWith(q)) score += 400;

    // Substring match
    if (title.includes(q)) score += 250;
    if (sub.includes(q))   score += 120;
    if (hay.includes(q))   score += 60;

    // Token coverage
    const tokens = q.split(/\s+/).filter(Boolean);
    let covered = 0;
    for (const t of tokens) {
      if (title.includes(t)) { score += 80; covered++; continue; }
      if (sub.includes(t))   { score += 35; covered++; continue; }
      if (hay.includes(t))   { score += 15; covered++; }
    }
    // Reward matching more tokens
    score += covered * 10;

    // Tiny preference: Articles > Projects > Results only when scores equal
    if (item.type === 'Article') score += 3;
    if (item.type === 'Project') score += 2;
    if (item.type === 'Result')  score += 1;

    return score;
  }

  function sortByRelevance(items, q){
    const qq = normalize(q);
    return items
      .map(it => ({ it, s: scoreItem(it, qq) }))
      .filter(x => qq ? x.s > 0 : true)
      .sort((a,b) => {
        if (b.s !== a.s) return b.s - a.s;
        // If same score, prefer newer date (if available)
        const ad = a.it.date || '';
        const bd = b.it.date || '';
        if (bd !== ad) return bd.localeCompare(ad);
        return (a.it.title || '').localeCompare(b.it.title || '');
      })
      .map(x => x.it);
  }

  function render(items, q){
    results.innerHTML = '';

    const total = items.length;
    const shown = Math.min(total, 50);

    if (!q) {
      meta.textContent = `${total} items`;
    } else {
      meta.textContent = total ? `${total} results` : 'No results';
    }

    if (!total) {
      results.innerHTML = `
        <div class="x-result x-result--empty" role="status">
          <div class="x-result__body">
            <div class="x-result__title">Nothing found</div>
            <div class="x-result__sub">Try different keywords (e.g. “braking”, “python”, “aero”, “monza”).</div>
          </div>
        </div>
      `;
      return;
    }

    for (const item of items.slice(0, 50)) {
      const card = document.createElement('a');
      card.className = 'x-result';
      card.href = item.url;

      const media = document.createElement('div');
      media.className = 'x-result__media';

      if (item.hero) {
        const img = document.createElement('img');
        img.loading = 'lazy';
        img.decoding = 'async';
        img.src = item.hero;
        img.alt = item.title || '';
        media.appendChild(img);
      } else {
        media.innerHTML = '<div class="x-result__ph"></div>';
      }

      const body = document.createElement('div');
      body.className = 'x-result__body';

      const type = escapeHtml(item.type || '');
      const title = escapeHtml(item.title || '');
      const subtitle = escapeHtml(item.subtitle || '');
      const date = escapeHtml(item.date || '');

      body.innerHTML = `
        <div class="x-result__top">
          <span class="x-pill">${type}</span>
          ${date ? `<span class="x-date">${date}</span>` : ''}
        </div>
        <div class="x-result__title">${title}</div>
        ${subtitle ? `<div class="x-result__sub">${subtitle}</div>` : ''}
      `;

      card.appendChild(media);
      card.appendChild(body);
      results.appendChild(card);
    }

    if (total > shown) {
      const more = document.createElement('div');
      more.className = 'x-muted';
      more.style.marginTop = '12px';
      more.textContent = `Showing ${shown} of ${total}. Refine your search to narrow down.`;
      results.appendChild(more);
    }
  }

  // Debounce for perceived smoothness
  function debounce(fn, wait){
    let t = null;
    return function(...args){
      window.clearTimeout(t);
      t = window.setTimeout(() => fn.apply(this, args), wait);
    };
  }

  function run(){
    const q = input.value || '';
    const qq = normalize(q);

    setQueryParam(q.trim());

    if (!qq) {
      const items = unique
        .slice()
        .sort((a,b) => (b.date || '').localeCompare(a.date || ''));
      render(items, '');
      return;
    }

    const ranked = sortByRelevance(unique, q);
    render(ranked, q);
  }

  // Init
  const initial = parseQuery();
  input.value = initial;
  input.focus({ preventScroll: true });

  const runDebounced = debounce(run, 60);
  input.addEventListener('input', runDebounced);

  // ESC clears query fast
  input.addEventListener('keydown', (e) => {
    if (e.key === 'Escape') {
      input.value = '';
      run();
    }
  });

  run();
})();
</script>