---
layout: page
permalink: /publications/
title: publications
nav: true
nav_order: 3
description: Publications from the lab, newest first.
---

<!-- _pages/publications.md -->

{%- comment -%}
The lab was founded in 2026 and its own publications are still in flight.
Work the PI published beforehand lives on the personal homepage by design and
is deliberately not mirrored here.

To publish from here, add entries to _bibliography/papers.bib: jekyll-scholar
renders them below, grouped by year, with Bib / PDF / code buttons. The search
box and the bibliography render themselves once there is anything to show.
{%- endcomment -%}

{% include drxs/empty_state.liquid message="The lab's first publications are on their way." hint="Work published before the lab was founded is listed on the PI's homepage." %}

<p style="margin-top: 1.25rem; text-align: center">
  <a class="drxs-btn drxs-btn-secondary" href="{{ site.data.lab.pi_homepage }}">
    PI's publications
    <span class="drxs-btn-zh">PI 个人主页论文列表</span>
  </a>
</p>

<div class="publications">
  {% bibliography %}
</div>
