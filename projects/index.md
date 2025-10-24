---
layout: page
title: Research projects
---

<div class="projects-grid" id="projectsGrid">
  {%- assign items = site.projects | sort: "year" | reverse -%}
  {%- for p in items -%}
    {%- include project-card.html p=p -%}
  {%- endfor -%}
</div>
