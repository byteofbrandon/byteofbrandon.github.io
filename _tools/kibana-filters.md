---
layout: archive
author_profile: true
custom_css: /assets/css/custom_css
header:
  overlay_color: "#000"
  overlay_filter: "0.4"
  overlay_image: /assets/images/banner.png
  height: 600px
  caption: >
    <div style="text-align: left; padding-left: 2rem; max-width: 600px;">
      <h1 style="margin-bottom: 0.3rem; color: #00ffd5; font-family: 'Fira Code', monospace;">Kibana Filters Overview</h1>
      <p style="margin-top: 0; color: #ccc; font-family: 'Fira Code', monospace;">Mastering data filtering and query techniques</p>
    </div>
title: "Kibana Filters Overview"
tags: [kibana, filters, tools]
last_updated: 2025-06-10
---

<style>
h1, h2, h3, h4 {
  color: #00ffd5;
  font-family: 'Fira Code', monospace;
}

p {
  color: #cccccc;
  font-family: 'Fira Code', monospace;
}

a {
  color: #00ffd5;
  text-decoration: underline;
}

a:hover {
  color: #ff4cf0;
}

body {
  background-color: #0f0f0f;
}

hr {
  border-color: #00ffd5;
}

.content-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.archive {
  width: 100% !important;
  max-width: none !important;
}

.page__content {
  width: 100% !important;
  max-width: none !important;
}

.filter-section {
  background: rgba(0, 255, 213, 0.05);
  border-left: 4px solid #00ffd5;
  padding: 1.5rem;
  margin: 1.5rem 0;
  border-radius: 0 8px 8px 0;
}

.filter-section2 {
  background: rgba(0, 215, 255, 0.05);
  border-left: 4px solid #00ffd5;
  padding: 1.5rem;
  margin: 1.5rem 0;
  border-radius: 0 8px 8px 0;
}

.code-block {
  background: rgba(0, 0, 0, 0.6);
  border: 1px solid #333;
  border-radius: 4px;
  padding: 1rem;
  font-family: 'Fira Code', monospace;
  color: #00ffd5;
  overflow-x: auto;
}

.tip-box {
  background: rgba(255, 76, 240, 0.1);
  border: 1px solid #ff4cf0;
  border-radius: 8px;
  padding: 1rem;
  margin: 1rem 0;
}

.tip-box h4 {
  color: #ff4cf0;
  margin-top: 0;
}
/* Add bold styling */
strong, b {
  color: #00ffd5;
  font-weight: bold;
}
</style>

<div class="content-wrapper">

<div class="filter-section">

<strong style="color: #00ffd5; font-weight: bold;">Fuzzy Searches</strong><br>
Find results similar to query<br>
Ex: host_name:server01~1<br>
Will match results with one level of deviance (servor)  

</div>

<div class="filter-section2">

<strong style="color: #00ffd5; font-weight: bold;">Proximity Searches</strong><br>
Find results with keywords in a set proximity of eachother<br>
Ex: log_message:"server error"~1<br>
Will match results with "servor" and "error" 1 word or less from eachother  

</div>

<div class="filter-section">

<strong style="color: #00ffd5; font-weight: bold;">Regular Expressions</strong><br>
Wrap regular expressions in forward slashes<br>
Ex: event_type:/.*/<br>
  
</div>


<div class="code-block">
Last 24 hours<br>
@timestamp:[now-24h TO now]<br>

Specific date range<br>
@timestamp:[2025-06-01 TO 2025-06-10]<br>
@timestamp<yyyy-MM-dd
</div>

---


</div>