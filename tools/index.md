---
layout: page_custom
title: Tools
description: Helpful tools from my cyber journey.
permalink: /tools/
---
<ul>
  {% for item in site.tools %}
    <li><a href="{{ item.url }}">{{ item.title }}</a></li>
  {% endfor %}
</ul>
