---
layout: page
permalink: /news/
title: news
nav: true
nav_order: 4
description: 新闻动态 · What's happening in the lab
---

{%- comment -%}
Reverse-chronological news feed with category filtering.

Items live in _news/*.md. Each may set `category:` (one of the ids in
`categories` below), `summary:` for the excerpt, and `cover:` for a lead
image. Items with `inline: true` render in place; others link to their own
generated page at /news/<slug>/.
{%- endcomment -%}

{%- assign categories = 'group,award,media,event' | split: ',' -%}
{%- assign category_labels = 'Lab news 组内新闻,Awards 学术获奖,Media 媒体报道,Events 学术活动' | split: ',' -%}

<div class="drxs-news-filters" role="group" aria-label="Filter news by category">
  <button class="drxs-filter-btn" type="button" data-filter="all" aria-pressed="true">All 全部</button>
  {%- for cat in categories %}
    <button class="drxs-filter-btn" type="button" data-filter="{{ cat }}" aria-pressed="false">
      {{ category_labels[forloop.index0] }}
    </button>
  {%- endfor %}
</div>

{%- assign news_items = site.news | sort: 'date' | reverse -%}

{%- if news_items.size > 0 %}
  <div class="drxs-news-list">
    {%- for item in news_items %}
      {%- assign cat = item.category | default: 'group' -%}
      <article class="drxs-news-item{% if item.cover %} has-cover{% endif %}" data-category="{{ cat }}">
        <div>
          <time class="drxs-news-date" datetime="{{ item.date | date_to_xmlschema }}">{{ item.date | date: '%b %d, %Y' }}</time>
          <span class="drxs-news-category">{{ cat }}</span>
        </div>

        <div>
          {%- if item.inline %}
            <div class="drxs-news-excerpt" style="margin-top: 0">{{ item.content | emojify }}</div>
          {%- else %}
            <h2 class="drxs-news-title">
              <a href="{{ item.url | relative_url }}">{{ item.title }}</a>
            </h2>
            {%- if item.summary %}
              <p class="drxs-news-excerpt">{{ item.summary }}</p>
            {%- endif %}
            <a class="drxs-news-more" href="{{ item.url | relative_url }}">Read more →</a>
          {%- endif %}
        </div>

        {%- if item.cover %}
          <div class="drxs-news-cover">
            <img src="{{ item.cover | prepend: '/assets/img/' | relative_url }}" alt="{{ item.title }}" loading="lazy">
          </div>
        {%- endif %}
      </article>
    {%- endfor %}

  </div>

  <div class="drxs-empty" id="drxs-news-none" hidden>
    <p>No news in this category yet.</p>
  </div>
{%- else %}
  {% include drxs/empty_state.liquid message="No news yet." %}
{%- endif %}

<script>
  // Category filtering. Progressive enhancement: without JS every item is
  // already visible in the markup and the buttons simply do nothing.
  (function () {
    var buttons = document.querySelectorAll(".drxs-filter-btn");
    var items = document.querySelectorAll(".drxs-news-item");
    var noneMessage = document.getElementById("drxs-news-none");
    if (!buttons.length || !items.length) return;

    function apply(filter) {
      var shown = 0;
      items.forEach(function (item) {
        var match = filter === "all" || item.dataset.category === filter;
        item.hidden = !match;
        if (match) shown++;
      });
      if (noneMessage) noneMessage.hidden = shown > 0;
    }

    buttons.forEach(function (button) {
      button.addEventListener("click", function () {
        buttons.forEach(function (other) {
          other.setAttribute("aria-pressed", String(other === button));
        });
        apply(button.dataset.filter);
      });
    });
  })();
</script>
