---
layout: page
permalink: /research/
title: research
nav: true
nav_order: 1
description: >
  Our work centers on the safety of robot interaction — how robots can act in physical contact with people and objects without putting them at
  risk. We pursue it along four connected directions, from the mechanisms of human motion, through perception and control at the moment of contact,
  to the policies and the hardware that make safe interaction possible in the first place.
---

{% for d in site.data.research %}
  <section class="drxs-research-block" id="{{ d.id }}">
    <h2 class="drxs-research-title">
      {{ d.name_en }}
      <span class="drxs-research-title-zh">{{ d.name_zh }}</span>
    </h2>

    {%- if d.tags %}
      <ul class="drxs-tags">
        {%- for tag in d.tags %}
          <li class="drxs-tag">{{ tag }}</li>
        {%- endfor %}
      </ul>
    {%- endif %}

    <div class="drxs-research-body">
      {%- for para in d.background %}
        {{ para | markdownify }}
      {%- endfor %}
    </div>

    <!-- Representative papers -->
    <h3 class="drxs-subheading">Representative work</h3>
    {%- if d.papers and d.papers.size > 0 %}
      <ul class="drxs-paper-list">
        {%- for p in d.papers %}
          <li>
            {%- if p.url %}
              <a href="{{ p.url }}">{{ p.title }}</a>
            {%- else %}
              {{ p.title }}
            {%- endif %}
            <span class="drxs-paper-meta">— {{ p.venue }}{% if p.year %} {{ p.year }}{% endif %}</span>
          </li>
        {%- endfor %}
      </ul>
    {%- else %}
      {% include drxs/empty_state.liquid message="Papers in this direction will be listed here as they appear." %}
    {%- endif %}

    {%- comment -%}
      No per-direction "People" list: members are shown on the Team page only.
      The `members:` field in _data/research.yml is therefore unused for now.
    {%- endcomment -%}

    <!-- Optional: open-source projects and datasets -->
    {%- if d.resources and d.resources.size > 0 %}
      <h3 class="drxs-subheading">Code &amp; data</h3>
      <div class="drxs-featured-links">
        {%- for r in d.resources %}
          <a class="drxs-link-chip" href="{{ r.url }}">{{ r.label }}</a>
        {%- endfor %}
      </div>
    {%- endif %}

  </section>
{% endfor %}
