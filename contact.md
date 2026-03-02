---
layout: page
title: Contact
permalink: /contact/
---

<section class="x-page">
  <div class="x-wrap">
    <h1 class="x-h1">Contact</h1>
    <p class="x-muted">Quick links for collaboration, opportunities, and team work.</p>

    <div class="x-grid x-grid--2">
      <article class="x-card" id="linkedin">
        <div class="x-card__body">
          <h3 class="x-card__title">LinkedIn</h3>
          {% if site.social and site.social.linkedin and site.social.linkedin != "" %}
            <p class="x-card__sub">Connect on LinkedIn.</p>
            <a class="u-btn u-btn--primary" href="{{ site.social.linkedin }}" target="_blank" rel="noreferrer noopener">Open LinkedIn</a>
          {% else %}
            <p class="x-card__sub">Set your LinkedIn URL in <code>_config.yml</code> → <code>social.linkedin</code>.</p>
          {% endif %}
        </div>
      </article>

      <article class="x-card" id="instagram">
        <div class="x-card__body">
          <h3 class="x-card__title">Instagram</h3>
          {% if site.social and site.social.instagram and site.social.instagram != "" %}
            <p class="x-card__sub">Follow the latest updates.</p>
            <a class="u-btn u-btn--primary" href="{{ site.social.instagram }}" target="_blank" rel="noreferrer noopener">Open Instagram</a>
          {% else %}
            <p class="x-card__sub">Set your Instagram URL in <code>_config.yml</code> → <code>social.instagram</code>.</p>
          {% endif %}
        </div>
      </article>

      <article class="x-card" id="email">
        <div class="x-card__body">
          <h3 class="x-card__title">Email</h3>
          {% if site.social and site.social.email and site.social.email != "" %}
            <p class="x-card__sub">Best for opportunities and longer messages.</p>
            <a class="u-btn u-btn--primary" href="mailto:{{ site.social.email }}">{{ site.social.email }}</a>
          {% else %}
            <p class="x-card__sub">Set your email in <code>_config.yml</code> → <code>social.email</code>.</p>
          {% endif %}
        </div>
      </article>
    </div>
  </div>
</section>
