---
layout: collection_index
title: "Scripts"
---

# Scripts

<ul>
  {% for item in site.scripts %}
  <li><a href="{{ item.url }}">{{ item.title }}</a></li>
  {% endfor %}
</ul>
