---
layout: page
title: AI & UX projects
nav_order: 3
---

<div>
Selected projects applying behavioral science, UX research, data analysis, and AI prototyping to design tools for reflection, learning, social understanding, and decision-making.
</div>

{%- assign items = site.ux_projects | sort: "order" -%}

<div class="projects-grid" id="uxProjectsGrid">
  {%- for p in items -%}
    {%- include project-card.html p=p -%}
  {%- endfor -%}
</div>
