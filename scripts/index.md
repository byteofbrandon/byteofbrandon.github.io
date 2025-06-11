---
layout: page_custom
title: Scripts
description: Scripts I’ve written or found useful in cybersecurity.
permalink: /scripts/
---
<ul>
  {% for item in site.scripts %}
    <li><a href="{{ item.url }}">{{ item.title }}</a></li>
  {% endfor %}
</ul>
