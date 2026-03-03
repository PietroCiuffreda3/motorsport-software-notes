---
layout: default
title: Results
permalink: /results/
---

<div class="u-wrapper">
  <h1 class="u-section-title">Results</h1>
  <p class="u-lead">A structured log of race weekends, deliverables, and measurable outcomes. Not a trophy wall.</p>

  {% assign stints = site.results | group_by: 'stint_id' %}
  {% for stint in stints %}
    {% assign meta = stint.items | first %}
    <section class="u-stint" aria-label="{{ meta.team_name }} stint">
      <header class="u-stint__header">
        <img src="{{ '/assets/teams/logo_SiLo.jpg' | relative_url }}" alt="SiLo Racing logo">loading="lazy">
        <div class="u-stint__meta">
          <div class="u-stint__title">{{ meta.team_name }}</div>
          <div class="u-stint__dates">
            {{ meta.stint_start | date: "%b %-d, %Y" }} → {{ meta.stint_end }}
          </div>
        </div>
      </header>

      <div class="u-results-grid">
        {% assign items_sorted = stint.items | sort: 'date' | reverse %}
        {% for r in items_sorted %}
          <article class="u-news-card u-result-card">
            <a class="u-result-card__media" href="{{ r.url | relative_url }}" aria-label="{{ r.title }} details">
              {% if r.cover %}
                <img src="{{ r.cover | relative_url }}" alt="{{ r.title }} cover" loading="lazy">
              {% else %}
                <img src="{{ '/assets/cover/notes.jpg' | relative_url }}" alt="{{ r.title }} cover" loading="lazy">
              {% endif %}
            </a>
            <div class="u-result-card__body">
              <div class="u-result-card__top">
                <div class="u-result-card__event">{{ r.title }}</div>
                <div class="u-result-card__date">{{ r.date | date: "%b %-d, %Y" }}</div>
              </div>
              {% if r.subtitle %}<div class="u-result-card__sub">{{ r.subtitle }}</div>{% endif %}
              {% if r.outcome %}<div class="u-result-card__outcome">{{ r.outcome }}</div>{% endif %}
            </div>
          </article>
        {% endfor %}
      </div>
    </section>
  {% endfor %}
</div>
