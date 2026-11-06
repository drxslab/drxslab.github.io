---
layout: page
permalink: /join/
title: join us
nav: true
nav_order: 5
description: 加入我们 · Open positions at DrXs Lab
# The site-wide recruiting banner would point at this page, so it is suppressed.
recruit_banner: false
---

{%- assign join = site.data.join -%}
{%- assign lab = site.data.lab -%}

<div class="drxs-section-lead" style="max-width: 48rem">{{ join.intro | markdownify }}</div>

<!-- Open roles: one line rather than a section per role -->
<section class="drxs-open-roles">
  <h2 class="drxs-section-title">
    Open Positions
    <span class="drxs-section-title-zh">开放岗位</span>
  </h2>
  <p class="drxs-open-roles-line">
    We are currently recruiting {{ join.open_roles_en }}.
    <span class="drxs-open-roles-zh">我们正在招收{{ join.open_roles_zh }}。</span>
  </p>
</section>

<!-- How to apply -->
<section class="drxs-section" id="how-to-apply">
  <div class="drxs-section-header">
    <h2 class="drxs-section-title">
      How to Apply
      <span class="drxs-section-title-zh">申请说明</span>
    </h2>
  </div>

{%- comment -%}
    Language tabs, Chinese first — same pattern as the FAQ below. Both panels
    are in the markup and toggled with `hidden`, so the Chinese panel still
    shows if JavaScript never runs.
{%- endcomment -%}
  <div class="drxs-lang-tabs" role="tablist" aria-label="Application language">
    <button class="drxs-lang-tab" type="button" role="tab" id="apply-tab-zh" aria-controls="apply-panel-zh" aria-selected="true">中文</button>
    <button class="drxs-lang-tab" type="button" role="tab" id="apply-tab-en" aria-controls="apply-panel-en" aria-selected="false">English</button>
  </div>

  <div class="drxs-apply-panel" id="apply-panel-zh" role="tabpanel" aria-labelledby="apply-tab-zh">
    <h3 class="drxs-subheading">申请材料</h3>
    <ul>
      {%- for item in join.materials_zh %}
        <li>{{ item }}</li>
      {%- endfor %}
    </ul>

    <div class="drxs-apply-box">
      <p style="margin-top: 0">
        请将材料发送至
        <strong><a href="mailto:{{ join.how_to_apply.email }}">{{ join.how_to_apply.email }}</a></strong>
        ，邮件标题请使用：
      </p>
      <p><code>{{ join.how_to_apply.subject_format | escape }}</code></p>
      <ul style="margin-bottom: 0">
        {%- for note in join.how_to_apply.notes_zh %}
          <li>{{ note }}</li>
        {%- endfor %}
      </ul>
    </div>

  </div>

  <div class="drxs-apply-panel" id="apply-panel-en" role="tabpanel" aria-labelledby="apply-tab-en" hidden>
    <h3 class="drxs-subheading">What to send</h3>
    <ul>
      {%- for item in join.materials_en %}
        <li>{{ item }}</li>
      {%- endfor %}
    </ul>

    <div class="drxs-apply-box">
      <p style="margin-top: 0">
        Send everything to
        <strong><a href="mailto:{{ join.how_to_apply.email }}">{{ join.how_to_apply.email }}</a></strong>
        with the subject line:
      </p>
      <p><code>{{ join.how_to_apply.subject_format | escape }}</code></p>
      <ul style="margin-bottom: 0">
        {%- for note in join.how_to_apply.notes_en %}
          <li>{{ note }}</li>
        {%- endfor %}
      </ul>
    </div>

  </div>
</section>

<!-- FAQ -->
<section class="drxs-section" id="faq">
  <div class="drxs-section-header">
    <h2 class="drxs-section-title">
      Frequently Asked Questions
      <span class="drxs-section-title-zh">常见问题</span>
    </h2>
  </div>

{%- comment -%}
    Language tabs, Chinese first. Both panels are in the markup and toggled with
    the `hidden` attribute, so without JavaScript the Chinese panel is still
    shown and the English one is simply reachable by nothing — no blank section.
{%- endcomment -%}
  <div class="drxs-lang-tabs" role="tablist" aria-label="FAQ language">
    <button class="drxs-lang-tab" type="button" role="tab" id="faq-tab-zh" aria-controls="faq-panel-zh" aria-selected="true">中文</button>
    <button class="drxs-lang-tab" type="button" role="tab" id="faq-tab-en" aria-controls="faq-panel-en" aria-selected="false">English</button>
  </div>

  <div class="drxs-faq-panel" id="faq-panel-zh" role="tabpanel" aria-labelledby="faq-tab-zh">
    {%- for item in join.faq_zh %}
      <details class="drxs-faq-item">
        <summary>{{ item.q }}</summary>
        <div>{{ item.a | markdownify }}</div>
      </details>
    {%- endfor %}
  </div>

  <div class="drxs-faq-panel" id="faq-panel-en" role="tabpanel" aria-labelledby="faq-tab-en" hidden>
    {%- for item in join.faq_en %}
      <details class="drxs-faq-item">
        <summary>{{ item.q }}</summary>
        <div>{{ item.a | markdownify }}</div>
      </details>
    {%- endfor %}
  </div>
</section>

<script>
  // FAQ language tabs. Progressive enhancement: the Chinese panel is visible in
  // the markup, so this only adds the ability to switch.
  (function () {
    // Scoped per tablist: the page has two independent groups (apply and FAQ),
    // so a click must only switch the group it belongs to.
    document.querySelectorAll('[role="tablist"]').forEach(function (list) {
      var tabs = list.querySelectorAll(".drxs-lang-tab");
      tabs.forEach(function (tab) {
        tab.addEventListener("click", function () {
          tabs.forEach(function (other) {
            var selected = other === tab;
            other.setAttribute("aria-selected", String(selected));
            var panel = document.getElementById(other.getAttribute("aria-controls"));
            if (panel) panel.hidden = !selected;
          });
        });
      });
    });
  })();
</script>

<!-- PI contact -->
<section class="drxs-section" id="contact">
  <div class="drxs-section-header">
    <h2 class="drxs-section-title">
      Contact
      <span class="drxs-section-title-zh">联系方式</span>
    </h2>
  </div>

  <p>
    <strong>{{ site.data.team.pi.name_en }} ({{ site.data.team.pi.name_zh }})</strong><br>
    {{ site.data.team.pi.title_en }}, {{ lab.institute_en }}, {{ lab.university_en }}<br>
    <a href="mailto:{{ lab.contact.email }}">{{ lab.contact.email }}</a> ·
    <a href="{{ lab.pi_homepage }}">{{ lab.pi_homepage | remove: 'https://' }}</a><br>
    {{ lab.contact.address_en }}
  </p>
</section>
