---
layout: page
title: UX & data projects
---

<div>
Here are some projects beyond my research at USC. Using mixed methods, I hope to create products that help people better understand themselves and make more adaptive decisions.
</div>

{%- assign items = site.ux_projects | sort: "order" -%}

<div class="projects-grid" id="uxProjectsGrid">
  {%- for p in items -%}
    {%- include project-card.html p=p -%}
  {%- endfor -%}
</div>