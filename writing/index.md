---
layout: page
title: Writing
---

{%- assign items = site.writings | sort: "date" | reverse -%}

<div class="writing-list">
  {%- for a in items -%}
  <article class="writing-item">
    <div class="writing-text">
      <h3 class="writing-title">
        {% if a.external_url %}
          <a href="{{ a.external_url }}" target="_blank" rel="noopener">{{ a.title }}</a>
        {% else %}
          <a href="{{ a.url | relative_url }}">{{ a.title }}</a>
        {% endif %}
      </h3>

      {%- if a.date -%}
        <div class="writing-date">{{ a.date | date: "%b %e, %Y" }}</div>
      {%- endif -%}

      {%- if a.summary -%}
        <p class="writing-summary">{{ a.summary }}</p>
      {%- endif -%}

      {% if a.tags and a.tags.size > 0 %}
        <div class="writing-tags">
          {% for t in a.tags %}
            <span class="tag-pill">{{ t }}</span>
          {% endfor %}
        </div>
      {% endif %}
    </div>

    {% if a.thumb %}
      <div class="writing-thumb">
        <img src="{{ a.thumb | relative_url }}"
             alt="{{ a.thumb_alt | default: a.title | escape }}"
             loading="lazy">
      </div>
    {% endif %}
  </article>
  {%- endfor -%}
</div>