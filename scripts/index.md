---
layout: home
title: "Scripts"
permalink: /scripts/
---

# Scripts

<ul>
  {% for item in site.scripts %}
  <li><a href="{{ item.url }}">{{ item.title }}</a></li>
  {% endfor %}
</ul>
