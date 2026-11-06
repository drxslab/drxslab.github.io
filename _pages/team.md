---
layout: page
permalink: /team/
title: team
nav: true
nav_order: 2
---

{%- assign pi = site.data.team.pi -%}

<!-- Principal investigator -->
<section class="drxs-pi">
  <div class="drxs-pi-photo">
    {%- comment -%}
      figure.liquid needs a path relative to the site root, not to assets/img/:
      it derives the imagemagick webp srcset from exactly this string, so a bare
      filename yields /name-480.webp and every variant 404s.
    {%- endcomment -%}
    {%- assign pi_photo = pi.avatar | prepend: 'assets/img/' -%}
    {%
      include figure.liquid
      loading="eager"
      path=pi_photo
      class="img-fluid rounded-circle z-depth-1"
      alt=pi.name_en
    %}
  </div>

  <div>
    <h2 class="drxs-pi-name">
      {{ pi.name_en }}
      <span class="drxs-pi-name-zh">{{ pi.name_zh }}</span>
    </h2>
    <p class="drxs-pi-title">
      {{ pi.title_en }} · {{ pi.title_zh }}<br>
      {{ pi.affiliation_en }}
    </p>

    <div class="drxs-icon-row">
      <a href="mailto:{{ pi.email }}" title="Email" aria-label="Email {{ pi.name_en }}">
        <i class="fa-solid fa-envelope" aria-hidden="true"></i>
      </a>
      <a href="{{ pi.homepage }}" title="Homepage" aria-label="{{ pi.name_en }}'s homepage">
        <i class="fa-solid fa-link" aria-hidden="true"></i>
      </a>
      <a href="{{ pi.scholar }}" title="Google Scholar" aria-label="{{ pi.name_en }} on Google Scholar">
        <i class="ai ai-google-scholar" aria-hidden="true"></i>
      </a>
      <a href="{{ pi.github }}" title="GitHub" aria-label="{{ pi.name_en }} on GitHub">
        <i class="fa-brands fa-github" aria-hidden="true"></i>
      </a>
    </div>

    {%- comment -%}
      The Team page stays compact: no bio paragraphs here. `pi.bio` is kept in
      _data/team.yml, and the full biography lives on the PI's homepage.
    {%- endcomment -%}

    {%- if pi.honors and pi.honors.size > 0 %}
      <ul class="drxs-honors">
        {%- for honor in pi.honors %}
          <li>{{ honor }}</li>
        {%- endfor %}
      </ul>
    {%- endif %}

  </div>
</section>

<!-- Current members, grouped by role in a fixed order -->
{% for group in site.data.team.groups %}
  <section class="drxs-section" id="{{ group.id }}">
    <div class="drxs-section-header">
      <h2 class="drxs-section-title">
        {{ group.title_en }}
        <span class="drxs-section-title-zh">{{ group.title_zh }}</span>
      </h2>
    </div>

    {%- if group.members and group.members.size > 0 %}
      <div class="drxs-member-grid">
        {%- for m in group.members %}
          {% include drxs/member_card.liquid member=m %}
        {%- endfor %}
      </div>
    {%- else %}
      {%
        include drxs/empty_state.liquid
        message="We are recruiting for this role."
        hint="See the Join Us page for what we are looking for and how to apply."
      %}
    {%- endif %}

  </section>
{% endfor %}

<!-- Alumni -->
<section class="drxs-section" id="alumni">
  <div class="drxs-section-header">
    <h2 class="drxs-section-title">
      Alumni
      <span class="drxs-section-title-zh">毕业去向</span>
    </h2>
  </div>

{%- assign alumni = site.data.team.alumni | sort: 'year' | reverse -%}
{%- if alumni.size > 0 %}
    <ul class="drxs-alumni-list">
      {%- for a in alumni limit: 10 %}
        <li>
          <strong>{{ a.name_en }}</strong>
          {%- if a.name_zh %}{{ a.name_zh }}{% endif %}
          <span class="drxs-alumni-dest">{{ a.degree }} {{ a.year }} — {{ a.destination }}</span>
        </li>
      {%- endfor %}
    </ul>

    {%- comment -%}
      Collapse the tail into a <details> once the list gets long, so the page
      stays scannable. Uses no JavaScript.
    {%- endcomment -%}
    {%- if alumni.size > 10 %}
      <details class="drxs-more">
        <summary>Show all {{ alumni.size }} alumni</summary>
        <ul class="drxs-alumni-list">
          {%- for a in alumni offset: 10 %}
            <li>
              <strong>{{ a.name_en }}</strong>
              {%- if a.name_zh %}{{ a.name_zh }}{% endif %}
              <span class="drxs-alumni-dest">{{ a.degree }} {{ a.year }} — {{ a.destination }}</span>
            </li>
          {%- endfor %}
        </ul>
      </details>
    {%- endif %}
{%- else %}
    {% include drxs/empty_state.liquid message="No alumni yet — the lab was founded in 2026." %}
{%- endif %}
</section>
